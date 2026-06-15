---
typ: cowork-chat
datum: 2026-06-10
projekt: Hermes Agent im VCP
---
# Hermes Agent: Einrichtung + Telegram-Anbindung

## Ergebnis
✅ **Hermes Agent läuft auf dem Hostinger VPS und ist über Telegram erreichbar.**

## Was gemacht wurde
1. **Neu-Deployment:** Admin-Passwort des ersten Deployments (`hermes-agent-n71e` → `-c8bg`) war verloren, Auslesen über Docker Manager/Terminal scheiterte → Projekt gelöscht und frisch aus dem Katalog deployt (traefik blieb stehen, nexos.ai/Oxylabs-Credits blieben erhalten). Neue Zugangsdaten in 1Password gespeichert.
2. **Dashboard-Login geklärt:** „Sign in Nous Research"-Maske = eigenes Hermes-Dashboard (Basic Auth), kein Nous-Konto nötig.
3. **Funktionstest CLI/Chat:** bestanden — Main Model `nexosai · Claude Sonnet 4.6` (über Hostinger-Credits, automatisch konfiguriert), v0.16.0, 11 Auxiliary Tasks auto.
4. **Telegram-Bot:** via @BotFather erstellt, User-ID via @userinfobot, im Dashboard unter CHANNELS eingetragen (Proxy-Feld leer), Gateway gestartet → Bot antwortet in Telegram.

## Offene Punkte / Empfehlungen
- [ ] `/sethome` im Telegram-Chat senden (Home Channel für Cron-Ergebnisse), falls noch nicht geschehen
- [ ] Approval-Modus prüfen (Tirith): `manual` empfohlen, solange Vertrauen aufgebaut wird
- [ ] nexos.ai-Credit-Stand gelegentlich prüfen (Docker Manager → Projekte) — bei 0 stoppt Hermes
- ⚠️ Telegram-Bot-Chats sind nicht E2E-verschlüsselt: keine Patientendaten, Zugangsdaten, gGmbH-Interna

## Referenzen
- VPS: srv1736087.hstgr.cloud · Docker Manager → Projekt `hermes-agent-*`
- Doku: hostinger.com/tutorials/how-to-set-up-hermes-agent · hermes-agent.nousresearch.com/docs

## Nachtrag (gleiche Session, abends)
- ✅ Erster Cron-Job in Hermes eingerichtet: **Morning Briefing Mo–Fr 7:00** per Telegram (Top-News DE Politik/Wirtschaft/Gesundheit · Wetter Bellheim · Medizin/Forschung · max. 15 Zeilen mit Quellen). Erste Ausgabe: Do 11.06., 7:00
- Architektur-Entscheidung: Obsidian-Aufgaben-Briefing bleibt **lokal** (Patientennamen!), Hermes liefert separates News-Briefing via Telegram. Cowork-Sandbox hat keinen Netzzugang zu Telegram/VPS — direkte Weiterleitung nicht möglich
- Idee für später (Parkplatz-Kandidat): Vault-Teilsync zum VPS, damit Hermes auch Aufgaben briefen kann — nur mit Datenschutz-Filter


---

## Fortsetzung
→ [[2026-06-15-Hermes-Dual-Setup-Tutorial]] (Tailscale + lokale Desktop-App auf Mac Studio)
