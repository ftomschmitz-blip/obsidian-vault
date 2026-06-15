---
typ: cowork-chat
datum: 2026-06-15
projekt: Hermes Agent im VCP
vorgaenger: "[[2026-06-10-Hermes-Telegram-Setup]]"
---
# Hermes Dual-Setup: VPS ↔ Mac Studio Desktop App (verifiziertes Tutorial)

> **Ziel:** Hermes läuft weiter 24/7 auf dem Hostinger-VPS (Cron + Telegram), aber zusätzlich kannst du vom Mac Studio aus über die native Desktop-App **denselben** Hermes-Backend bedienen — mit Chat, Skills-Manager, Cron-Übersicht, File-Browser. Verbindung läuft über Tailscale, kein offener Port im Internet.

## Verifizierung der ursprünglichen Anleitung (Stand 15.06.2026)

| Punkt aus der Anleitung               | Status | Quelle                                                                                                                     |
| ------------------------------------- | ------ | -------------------------------------------------------------------------------------------------------------------------- |
| Port `9119` für Dashboard             | ✅ stimmt | [Web Dashboard Docs](https://hermes-agent.nousresearch.com/docs/user-guide/features/web-dashboard)                         |
| Pfad `Settings → Gateway → Remote gateway` | ✅ stimmt | [Desktop App Docs](https://hermes-agent.nousresearch.com/docs/user-guide/desktop#connecting-to-a-remote-backend)            |
| Env-Var-Namen `HERMES_DASHBOARD_BASIC_AUTH_USERNAME/PASSWORD` | ✅ exakt so | [Web Dashboard Docs](https://hermes-agent.nousresearch.com/docs/user-guide/features/web-dashboard#usernamepassword-provider-no-oauth-idp) |
| Bind `--host <tailscale-ip>`          | ✅ stimmt, Nous nennt Tailscale explizit als „clean option" | [Desktop App Docs](https://hermes-agent.nousresearch.com/docs/user-guide/desktop#on-the-backend-the-remote-machine) |
| `install.sh` vom Hermes-Repo          | ⚠️ **für dich irrelevant** — dein VPS läuft über Hostinger Docker Catalog, nicht über Bare-Metal install.sh                |
| PM2/systemd Persistenz                | ⚠️ **für dich irrelevant** — Docker `--restart unless-stopped` übernimmt das                                                |
| v0.16+ auf beiden Seiten              | ✅ stimmt — bei jedem Update auf beiden Seiten gleichziehen                                                                  |
| Empfohlener Mac-Download              | ✅ DMG von [hermes-agent.nousresearch.com/desktop](https://hermes-agent.nousresearch.com/desktop), Apple-Silicon-Build vorhanden |
| OAuth (Nous Portal) vs. Basic Auth    | ℹ️ Nous empfiehlt für VPS eigentlich **OAuth Nous Portal**. Username/Password ist nur „okay" hinter VPN (Tailscale). Genau das ist unser Setup — passt. |

**⚠️ Punkt, den du in der ursprünglichen Anleitung doppelt prüfen solltest, bevor du ausführst:**
- Im Hostinger-Docker-Katalog-Deployment läuft das Dashboard u.U. nicht automatisch als eigener Container. Du musst in der Hostinger-Docker-Manager-Oberfläche schauen, ob es einen `hermes-dashboard`-Container gibt. Wenn nicht → manuell starten (siehe Phase 1b Schritt 4).

---

## Phase 1 — VPS-Basis ✅ ERLEDIGT (10.06.2026)

Siehe [[2026-06-10-Hermes-Telegram-Setup]]. Konkret bereits vorhanden:
- ✅ Hostinger-VPS `srv1736087.hstgr.cloud` mit Hermes-Agent v0.16.0 als Docker-Stack
- ✅ Main-Model `nexosai · Claude Sonnet 4.6` über Hostinger-Credits konfiguriert
- ✅ Dashboard mit Basic Auth läuft, Zugangsdaten in **1Password** (Eintrag „Hermes VPS Dashboard")
- ✅ Telegram-Bot via @BotFather angelegt + im Dashboard registriert, antwortet
- ✅ Cron „Morning Briefing Mo–Fr 7:00" läuft

→ **Hier nichts neu machen.**

---

## Phase 1b — Tailscale aufsetzen (4 Geräte)

Tailscale baut ein verschlüsseltes Mesh-VPN zwischen allen deinen Geräten. Jedes Gerät bekommt eine stabile `100.x.x.x`-IP. Damit kannst du das Hermes-Dashboard nur über das VPN erreichen, ohne dass Port 9119 ins Internet offen sein muss.

### 1b.1 Tailscale-Account anlegen

1. Browser → https://tailscale.com → „Get started for free"
2. Login mit Google (`f.tom.schmitz@gmail.com`) — kein extra Passwort
3. Nach Login landest du auf der Admin-Console: https://login.tailscale.com/admin/machines (noch leer)

### 1b.2 VPS in Tailscale aufnehmen

SSH auf den VPS:
```bash
ssh root@srv1736087.hstgr.cloud   # oder dein konfigurierter User
```

Tailscale installieren + starten:
```bash
curl -fsSL https://tailscale.com/install.sh | sh
sudo tailscale up
```
Der Befehl gibt eine URL aus (`https://login.tailscale.com/a/xxxx`) — diese URL **auf deinem Mac** im Browser öffnen, der bereits eingeloggt ist, und das Gerät bestätigen.

Tailscale-IP des VPS auslesen:
```bash
tailscale ip -4
# Beispiel-Output: 100.83.42.17
```
→ **Diese IP in 1Password notieren** als „Hermes VPS Tailscale IP".

### 1b.3 Tailscale auf Mac Studio + MacBook + iPhone

**Mac Studio (Apple Silicon):**
1. https://tailscale.com/download → „Download for macOS" → DMG laden
2. DMG öffnen, Tailscale.app in `/Applications` ziehen
3. Erststart → „Log in" → Browser öffnet sich → mit Google-Account anmelden → fertig
4. Status-Icon oben rechts in Menüleiste, Hover zeigt VPS in der Liste

**MacBook:** dasselbe wie Mac Studio.

**iPhone:**
1. App Store → „Tailscale" → Installieren
2. App öffnen → Log in → Google → fertig

### 1b.4 Konnektivität prüfen

Auf Mac Studio Terminal:
```bash
ping 100.83.42.17        # eingetragene Tailscale-IP des VPS
```
Sollte antworten. Falls nicht: Tailscale-App auf Mac → „Enabled" prüfen.

### 1b.5 Hermes-Dashboard an Tailscale-IP binden (Hostinger-Docker-Spezifikum)

**⚠️ Vorsichtig vorgehen — hier hängt der Erfolg.** Da dein Dashboard im Hostinger-Container läuft, hast du zwei Pfade. Erst beide ansehen, dann **eine** Variante umsetzen:

**Variante A (einfach, empfohlen für Tom): Dashboard-Container neu starten und Port nur auf Tailscale-Interface binden**

Auf dem VPS:
```bash
# 1. Tailscale-IP nochmal holen:
TS_IP=$(tailscale ip -4)
echo $TS_IP   # z.B. 100.83.42.17

# 2. Prüfen, ob es schon einen Dashboard-Container gibt:
docker ps -a | grep -i dashboard

# 3a. Falls JA: stoppen, entfernen, mit neuem Bind starten:
docker stop hermes-dashboard 2>/dev/null
docker rm   hermes-dashboard 2>/dev/null

docker run -d \
  --name hermes-dashboard \
  --restart unless-stopped \
  -v ~/.hermes:/opt/data \
  -p ${TS_IP}:9119:9119 \
  nousresearch/hermes-agent dashboard --no-open --host 0.0.0.0 --port 9119

# 3b. Falls NEIN (es lief nur die Gateway/CLI-Variante): denselben Befehl, frisch.
```
`-p ${TS_IP}:9119:9119` bindet den Port nur an die Tailscale-Schnittstelle. Damit ist 9119 weder ans öffentliche Internet noch an die Hostinger-LAN erreichbar.

**Variante B (sauberer, aber mehr Aufwand): Hostinger-Docker-Compose-File anpassen und über `traefik` im VCP routen.** Lohnt sich nur, wenn du sowieso HTTPS auf dem VPS willst. Für jetzt: **Variante A wählen**.

**Firewall absichern (immer):**
```bash
sudo ufw deny 9119          # blockiert Port 9119 nach außen, falls UFW aktiv
sudo ufw allow in on tailscale0
```

### 1b.6 Basic-Auth-Credentials im VPS verifizieren

Die Credentials, die du in 1Password unter „Hermes VPS Dashboard" hast, müssen in `~/.hermes/.env` stehen — Doku verlangt exakt diese Variablen:

```bash
grep HERMES_DASHBOARD ~/.hermes/.env
```
Erwarteter Output (mindestens):
```
HERMES_DASHBOARD_BASIC_AUTH_USERNAME=admin
HERMES_DASHBOARD_BASIC_AUTH_PASSWORD=<dein-passwort>
HERMES_DASHBOARD_BASIC_AUTH_SECRET=<32+ Zeichen base64>
```
**Fehlt der `SECRET`?** → Setzen, sonst wirst du nach jedem VPS-Reboot abgemeldet:
```bash
echo "HERMES_DASHBOARD_BASIC_AUTH_SECRET=$(openssl rand -base64 32)" >> ~/.hermes/.env
chmod 600 ~/.hermes/.env
docker restart hermes-dashboard
```

### 1b.7 Gate-Status prüfen

Vom Mac Studio Terminal (über Tailscale):
```bash
curl -s http://100.83.42.17:9119/api/status | jq '.auth_required, .auth_providers'
```
Erwartet: `true` und `["basic"]` (oder ähnlich, mit `"basic"` enthalten).

---

## Phase 2 — Hermes Desktop App auf dem Mac Studio installieren

### 2.1 Download

1. Browser auf Mac Studio → https://hermes-agent.nousresearch.com/desktop
2. „Download for macOS (Apple Silicon)" → DMG (ca. 200 MB)
3. DMG öffnen → Hermes.app in `/Applications` ziehen

### 2.2 Erststart

1. Hermes.app aus `/Applications` starten
2. Erststart-Dialog: macOS fragt „Hermes ist aus dem Internet geladen" → Öffnen
3. Onboarding-Overlay erscheint → unten **„Choose provider later"** wählen (du nutzt ja den VPS-Backend, kein lokales Backend)
4. App öffnet sich mit leerer Chat-Ansicht

> ℹ️ Beim ersten Start lädt Hermes den Electron-Runtime (~114 MB) plus einen kleinen Python-Stack nach `~/.hermes/`. Dauert 1–3 Min, Spinner zeigt „Build desktop app". Falls es hängt: `ELECTRON_MIRROR=https://npmmirror.com/mirrors/electron/ open -a Hermes`.

### 2.3 Version verifizieren

In der App: **Hermes-Menü → About** → Version sollte ≥ 0.16.0 sein.
Falls niedriger: Hermes-Menü → Check for Updates.

> **Wichtig:** VPS-Version und Desktop-Version müssen denselben Major.Minor haben (also beide 0.16.x). Bei VPS-Update auch Desktop nachziehen, sonst kann der Remote-Gateway WS-Handshake fehlschlagen (Close-Code 4403/4401).

---

## Phase 3 — Remote-Gateway in der Desktop-App konfigurieren

### 3.1 Settings öffnen

1. In Hermes-App: oben links auf das Zahnrad-Icon ODER `⌘ + ,`
2. Linke Sidebar → **Gateway**
3. Sektion **Remote gateway** öffnen

### 3.2 URL und Login eingeben

1. **Remote URL** Feld: `http://100.83.42.17:9119` (Tailscale-IP des VPS aus 1Password einsetzen — **nicht** `srv1736087.hstgr.cloud`, das wäre öffentlich!)
2. Button **„Sign in"** klicken
3. Credential-Dialog erscheint:
   - **Username:** `admin` (aus 1Password, Eintrag „Hermes VPS Dashboard")
   - **Password:** aus 1Password kopieren
4. **Save and reconnect**

### 3.3 Verbindung verifizieren

- Statusbar unten zeigt: „Connected to 100.83.42.17:9119" (oder ähnlich)
- Sidebar → **Cron** sollte deinen „Morning Briefing"-Job zeigen → Beweis, dass du wirklich am VPS-Backend hängst, nicht am lokalen
- Sidebar → **Messaging** sollte deinen Telegram-Channel als „connected" zeigen

### 3.4 Troubleshooting-Kurzliste

| Symptom                            | Ursache                              | Fix                                                                 |
| ---------------------------------- | ------------------------------------ | ------------------------------------------------------------------- |
| „Connection refused" / Timeout     | Tailscale auf VPS oder Mac aus       | `tailscale status` auf beiden, neu starten                          |
| 401 „Invalid credentials"          | falsches User/Passwort               | gegen 1Password gegenchecken, `curl /api/status` zeigt `auth_required:true` |
| Kein „Sign in" Button, fragt Token | Basic-Auth-Provider nicht aktiv      | `HERMES_DASHBOARD_BASIC_AUTH_USERNAME` + `_PASSWORD` in `.env` setzen, Container restart |
| Nach VPS-Reboot abgemeldet         | `BASIC_AUTH_SECRET` fehlt            | siehe Phase 1b.6                                                    |
| Logs lesen                         | —                                    | App: Settings → Gateway → Open logs **oder** `hermes logs gui -f`   |

---

## Phase 4 — Best Practices im Alltag

### Lokales vs. Remote Gateway — wann was?

- **Remote (VPS-Backend):** alles, was 24/7 laufen oder von unterwegs erreichbar sein soll → Cron, Telegram, Sessions die du auf iPhone und Mac fortsetzen willst, Skills die der VPS gebaut hat.
- **Lokal (Desktop-App eigener Backend):** wenn du sensiblen Code/Patientendaten **auf dem Mac Studio** verarbeiten willst, ohne dass irgendwas Richtung VPS oder Cloud geht. Profile umschalten (Settings → Profiles → New: „Lokal-Sensitiv"), das Profil hängt am lokalen Backend. **Klare Trennung halten.**

### Backups

VPS-seitig, am besten als wöchentlicher Cron:
```bash
ssh root@srv1736087.hstgr.cloud "docker exec hermes-agent hermes backup --output /opt/data/backups/hermes-$(date +%Y%m%d).zip"
```
Wenn du den Backup-Pfad im Hostinger-Container nicht kennst: alternativ
```bash
ssh root@srv1736087.hstgr.cloud "tar czf ~/hermes-backup-$(date +%Y%m%d).tar.gz ~/.hermes"
scp root@srv1736087.hstgr.cloud:~/hermes-backup-*.tar.gz ~/Backups/Hermes/
```
→ Damit hast du `.hermes/.env`, Sessions, Skills, Cron-Konfig gesichert. **Backup-Datei verschlüsselt ablegen** (1Password Tresor oder verschlüsseltes Volume).

### Cron-Jobs

Bleiben auf dem **VPS**, nicht auf der Desktop-App — Mac Studio läuft nicht 24/7. Wenn du in der Desktop-App im Cron-Pane einen Job anlegst, wird er gegen das **VPS-Backend** geschrieben (weil du remote angemeldet bist) — das ist gut so.

### Update-Routine

Etwa alle 2–4 Wochen:
1. VPS: `docker pull nousresearch/hermes-agent:latest && docker restart hermes-agent hermes-dashboard`
2. Mac: Hermes → Check for Updates → installieren
3. **Beide Versionen müssen 0.16.x oder beide 0.17.x sein** — nicht mixen.
4. Nach Update: einmal Telegram-Test, einmal Desktop-Login-Test.

---

## 🔒 Sicherheits-Box — was darf NICHT über Hermes/Telegram

> **Eigene Regel aus dem 10.06.2026-Chat, hier verschärft, weil das Dashboard jetzt Vollzugriff hat:**

| ❌ Niemals                                  | Begründung                                                                                          |
| ------------------------------------------ | --------------------------------------------------------------------------------------------------- |
| Patientennamen, Diagnosen, KV-Nummern      | Telegram-Bot-Chats nicht E2E, VPS-Speicher nicht DSGVO-konform für Patientendaten, AI-Provider sieht alles |
| Praxis-Logins (Tomedo, ePA, KIM)           | Credentials gehören in 1Password, niemals als Prompt                                                |
| gGmbH-Interna SüdpfalzDOCs (Geschäftszahlen, Personalia) | Trennung der 4 Hüte einhalten                                                              |
| Echte Bankverbindungen, Steuer-IDs         | nicht in einem Cloud-AI-Loop landen                                                                  |
| `~/.hermes/.env` Inhalt teilen / pasten     | Enthält API-Keys, Basic-Auth-Passwort, nexosai-Credentials                                          |
| Approval auf `off` setzen für Tirith       | Bei VPS-Backend mit Shell-Zugriff hochriskant — auf `manual` lassen, solange Vertrauen aufgebaut wird |

> ⚠️ Speziell: Wer das Hermes-Dashboard-Login hat, **kann auf dem VPS Shell-Befehle ausführen** (über die Approval-Queue). Basic-Auth-Passwort und Tailscale-Mesh sind die zwei Schichten, die das schützen. **Beides ernst nehmen.**

---

## Aktions-Checkliste für dich (zum Abhaken)

- [ ] Tailscale-Account angelegt
- [ ] Tailscale auf VPS installiert + `tailscale ip -4` notiert
- [ ] Tailscale auf Mac Studio installiert
- [ ] Tailscale auf MacBook installiert
- [ ] Tailscale auf iPhone installiert
- [ ] Mac → VPS Tailscale-Ping erfolgreich
- [ ] Dashboard-Container an Tailscale-IP gebunden (Variante A, Phase 1b.5)
- [ ] `HERMES_DASHBOARD_BASIC_AUTH_SECRET` in `~/.hermes/.env` gesetzt
- [ ] `ufw deny 9119` + `ufw allow in on tailscale0`
- [ ] `curl /api/status` zeigt `auth_required:true`, `"basic"` in Providern
- [ ] Hermes Desktop App auf Mac Studio installiert
- [ ] Settings → Gateway → Remote gateway konfiguriert
- [ ] Test: Cron-Pane zeigt „Morning Briefing"
- [ ] Backup-Routine eingerichtet (mindestens manueller Erstabzug)

---

## Was rückgängig gemacht werden kann

| Aktion                                     | Rollback                                                                       |
| ------------------------------------------ | ------------------------------------------------------------------------------ |
| Tailscale auf VPS                          | `sudo tailscale down && sudo apt remove tailscale`                             |
| Dashboard-Container neu gebunden (Phase 1b.5) | Alten Container wiederherstellen mit `-p 0.0.0.0:9119:9119` falls nötig (Achtung: dann offen) |
| `.env` ergänzt                              | Vorher Backup: `cp ~/.hermes/.env ~/.hermes/.env.bak-pre-tailscale`             |
| UFW Regeln                                  | `sudo ufw delete deny 9119` und `sudo ufw delete allow in on tailscale0`        |
| Desktop-App                                 | App in den Papierkorb, plus `rm -rf ~/.hermes/hermes-agent` (löscht nur lokalen Backend, nicht VPS) |

**Empfohlene Sicherung VOR den Aktionen:**
```bash
ssh root@srv1736087.hstgr.cloud "cp ~/.hermes/.env ~/.hermes/.env.bak-$(date +%Y%m%d) && tar czf ~/hermes-backup-pre-tailscale-$(date +%Y%m%d).tar.gz ~/.hermes"
```

---

## Referenzen

- Vorgänger: [[2026-06-10-Hermes-Telegram-Setup]]
- [Hermes Web Dashboard Docs](https://hermes-agent.nousresearch.com/docs/user-guide/features/web-dashboard)
- [Hermes Desktop App Docs](https://hermes-agent.nousresearch.com/docs/user-guide/desktop)
- [Hostinger Hermes-Tutorial](https://www.hostinger.com/tutorials/how-to-set-up-hermes-agent)
- [Tailscale Setup Guide für Hermes](https://openclawlaunch.com/guides/hermes-agent-tailscale) (Drittquelle, zur Doppelprüfung)
- [Tailscale Download](https://tailscale.com/download)
- VPS: `srv1736087.hstgr.cloud` · Hostinger Docker Manager → Projekt `hermes-agent-*`
- 1Password-Einträge: „Hermes VPS Dashboard", neu anzulegen: „Hermes VPS Tailscale IP"
