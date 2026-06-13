---
typ: faeden
aktualisiert: 2026-06-13
---
# 🧵 Handlungsfäden

Projekt-Ebene über dem [[00_Cockpit]]: Was läuft, was ist der nächste Schritt, was hat Priorität.

**Spielregeln:**
1. **Jede Claude-Session** (Code, Desktop, Cowork) aktualisiert am Ende ihren Faden-Block: Stand + Nächster Schritt.
2. **WIP-Limit: max. 7 aktive Fäden.** Neues landet im Parkplatz — aktiviert wird nur im Wochenreview.
3. **Wochenreview (15 Min, freitags oder sonntags):** Tom sagt in irgendeiner Claude-Session „Wochenreview bitte" → Claude liest diese Notiz, geht alle Fäden durch (Was ist passiert? Stockt etwas? Was fliegt raus?), gemeinsam werden die **Top-3 der Woche** neu gesetzt.

Status: 🔴 kritisch/dringend · 🟢 läuft · 🟡 stockt/wartet · ⏸️ geparkt

---

## ⭐ Top-3 dieser Woche *(vorläufig — im ersten Wochenreview bestätigen)*

1. **gGmbH:** Kontostand feststellen → Reichweite → Krisengespräch vorbereiten
2. **Praxis:** Q2/2026-Vorprüfung abarbeiten (Frist 30.06.!)
3. **Organisation:** Kalender-Woche (6-Hüte-Plan Woche 2) wiederholen

---

## Aktive Fäden

### 🔴 gGmbH Liquiditätskrise
- **Hut:** 50_gGmbH · **Stand:** 10.06. (abends) — Leitfaden v2 + rollierender Plan geprüft: Juni nur mit Stundung der Anwaltsrechnung gedeckt (sonst −659 €), Lücke bis 31.12. real 46–81 T€ (nicht 35–40). Krisengespräch im Sparring trainiert; Maßnahmenkatalog mit 10 Beschlusspunkten, Verantwortlichen und Fristen steht: [[Massnahmenkatalog-Liquiditaet-gGmbH-2026-06-10]]
- **Nächster Schritt:** StB-Anfrage §§ 17/18/15a/15b InsO binnen 48 h raus (Anlagen: BWA 04/2026 + Liquiditätsstatus) → Krisengespräch Vorstand terminieren
- **Danach:** Leitfaden-Einstieg auf korrigierte Juni-Lage anpassen · 13-Wochen-Plan-Sachkosten vom GF · Kreis-Termin (Betrauungsmittel)
- **Quellen:** [[2026-06-10-Krisengespraech-Training]] · [[2026-06-10-gGmbH-Liquiditaetskrise-Leitfaden]] · `~/Desktop/Claude /gGmbH Südpfalz/`

### 🔴 Praxis: KV-Abrechnung Q2/2026
- **Hut:** 10_Praxis-Bellheim · **Stand:** 12.06. — `kv_bellheim.py` rekonstruiert (VG-Erfassung jetzt 100 % statt 92,8 %), neuer KV-Datensatz vom 12.06. verarbeitet: Honorar 209.326,50 € (+12.951 ggü. 06.06.), Fallwert 86,46 €, 2.421 Fälle. Honorarwirksame Vorprüfungs-Treffer 38 → 10 — Korrekturen haben gegriffen. Dashboard + Aktionsliste + Snapshot-Vergleich im Projektordner; PDFs + tomedo-Exporte dort abgelegt.
- **Nächster Schritt:** Aktionsliste abarbeiten — 3 SKT-Scheine (Abdule, Bülbül, **neu: Al Humsi**), Fall Ruppender (kurative Diagnose), 6 GOP-Konflikte. **Kriterium 10 Sprechstundenzeiten im Mitgliederbereich auf „Ja" stellen (immer noch offen!)** + Video von 0,59 % auf ≥1 % (~10–11 Videofälle) → 03041 statt 03042 — **Frist 30.06.**
- **Danach:** tomedo-XLSX-Merge (Exporte liegen bereit: KV + EBM vom 12.06.), Chronikerquoten 03220/03221, Quartalsvergleich via Snapshots
- **Quellen:** [[2026-06-12-KV-Pipeline-Rekonstruktion]] · Projektordner `~/Documents/Claude/Projects/Praxis Assistent zur Datenanalyse  KV Abrechnungen/`

### 🟡 Organisation: 6-Hüte-Setup (Master-Plan v2)
- **Hut:** übergreifend · **Stand:** 10.06. (abends, Konsistenz-Audit) — Planfile jetzt vollständig auf v2 konsolidiert (v1-Reste in Roadmap/Tasks/Mailbox/Dateien-Abschnitten entfernt). Cross-App-Drift behoben: kanonische Quellen festgelegt (Planfile = Soll · dieser Faden = Stand · Memory = nur Verweis). Ist-Zustand erhoben: Erinnerungen noch 4 v1-Listen + 8 Alt-Listen („Erinnerungen Private" doppelt!), Kalender noch v1-Farben.
- **Nächster Schritt:** Kalender-Woche neu ansetzen (6 Hüte, RGB-Farbcode per AppleScript) + dabei Erinnerungen auf 6 v2-Listen migrieren
- **Quellen:** [[2026-06-10-Konsistenz-Audit-Claude-Umgebung]] · `~/Desktop/Claude /Projekte/Organisation/Master-Plan_Setup_2026-05.md`

- **Drift entdeckt (10.06., claude.ai-Browser-Session):** Projektwissen „Claude Optimierung" im Claude.ai-Projekt führt das Dispatch-Setup als komplett offen (alle Checkboxen leer), obwohl Dispatch seit Anfang Juni aktiv ist. Datei liegt weder im Vault noch unter `~/Documents/Claude/Projects` — nur als Projektwissen in der Claude.ai-UI, daher per MCP nicht korrigierbar. → **Tom:** Status-Block in der Projekt-UI durch Verweis auf [[00_Faeden]] ersetzen (Snippet aus Chat 10.06.)

### 🟡 Blitztext: Hotkeys zum Laufen bringen
- **Hut:** übergreifend · **Stand:** 10.06. — App läuft, Diktat per Menüleisten-Klick funktioniert (inkl. Auto-Paste). Hotkeys gehen nicht — Ursache gefunden: Belegung war falsch notiert, laut Code ist Transkription **`fn + Shift`** (nicht `fn` allein). `AppleFnUsageType` stand wieder auf 3, erneut auf 0 gesetzt.
- **Nächster Schritt:** `fn + Shift` halten → sprechen → loslassen testen. Falls tot: Bedienungshilfen-Berechtigung prüfen (Systemeinstellungen → Datenschutz & Sicherheit → Bedienungshilfen, alte Blitztext-Einträge entfernen, App neu starten)
- **Quellen:** [[2026-06-10-Blitztext-Hotkeys]] · `~/blitztext-app/BlitztextMac/Services/HotkeyService.swift`

### 🟢 Mail-System: Smart-Mailbox-Fixes
- **Hut:** übergreifend · **Stand:** 10.06. (spät) — **Weg A umgesetzt:** iCloud-Ordner `40 SüdpfalzDOCs` + 4 Unterordner angelegt, Regel auf iCloud-Ziel umgestellt (plist-verifiziert), Bestand verschoben: 3.474 + 92 = 3.566 Mails, lokale Quellordner leer (Index-verifiziert). Upload ~3,9 GB läuft asynchron — **Mac anlassen!** Outbox-Anomalie zuvor geklärt (verwaiste Kopien, 126/129 versendet). [[Mail-System]] mit Nachtrag + Undo-Log versehen.
- **Nächster Schritt:** (1) Morgen am iPhone prüfen: iCloud-Ordner 00–90 inkl. 40er-Inhalt sichtbar? (2) Tom: C. Weißler wegen „Fwd: Vorhaltepauschale" nachfassen. (3) Nach Sync-Bestätigung Aufräum-Freigabe: TEST_ICLOUD_FOLDER, leere lokale 00–90-Struktur, lokaler „iCloud"-Spiegelordner, Outbox-Altlasten → dann [[Mail-System]] konsolidieren
- **Quellen:** [[2026-06-10-Mail-Geraete-Harmonisierung]] · [[Mail-System]]

### 🟢 Hermes Agent im VCP
- **Hut:** übergreifend · **Stand:** 10.06. (abends) — Setup komplett: Hermes auf Hostinger VPS, Telegram-Gateway aktiv, `/sethome` gesetzt. Erster Cron-Job läuft: Morning Briefing Mo–Fr 7:00 per Telegram (News DE, Wetter Bellheim, Medizin-Update). Zugangsdaten in 1Password
- **Nächster Schritt:** Morgen (11.06.) prüfen, ob das erste Briefing um 7:00 ankommt und Qualität passt → danach weitere Use Cases. Oxylabs-Credits im Blick behalten (Websuche)
- **Regel:** keine Patientendaten/Zugangsdaten/gGmbH-Interna über den Bot (kein E2E)
- **Quellen:** [[2026-06-10-Hermes-Telegram-Setup]]

### 🟢 Token sparen: Lokaler Ollama-Direktzugang
- **Hut:** übergreifend · **Stand:** 13.06. — Denkmodell korrigiert: es gibt KEINEN „erst lokal, dann Claude"-Vorfilter; jede Claude-Session läuft voll über die Cloud (kostenpflichtig), Ollama nur wenn Claude das MCP-Tool aufruft. Echter Gratis-Weg = lokaler Direktkanal ohne Claude. **Open WebUI** installiert (`uv tool install --python 3.11 open-webui`, isoliert), verbunden mit headless `ollama serve`, läuft auf http://localhost:8080, Telemetrie aus, kein Autostart. Steuer-Skript `~/.local/bin/ollama-ui` (start/stop/status) angelegt + getestet (Health ✅).
- **Nächster Schritt Tom:** im Browser einmalig lokalen Admin-Account anlegen → Modell wählen (llama3.2/qwen3:8b/gemma4) → testen. Danach Faustregel im Alltag anwenden (reines Nachdenken über Text → lokal; etwas tun/nachschauen/koordinieren → Claude).
- **Spar-Haupthebel zusätzlich:** Session-Disziplin (neuer Chat pro Thema, /compact bei langen Threads).
- **Quellen:** [[2026-06-13-Lokaler-Ollama-Direktzugang]] · Memory `project_local_ollama_ui`

## ⏸️ Parkplatz


- **Downloads-Rest:** Cloud-Stubs prüfen + MS365-Ablage (aus Bereinigung 30.05.)
- **Festplatte:** nur noch 17 GB frei (97 %) — nächste Kandidaten: icloudmailagent (812 MB), Google-Cache (787 MB)
- **Obsidian-MCP:** recent_changes defekt — bei Gelegenheit fixen oder ersetzen
- **Sommerurlaub 2026 (06.–17.07.):** Phase 2 erledigt (10.06. abends) — Italsol + Sardinien gestrichen, Detailauswertung Le Torri vs. La Fenice in [[Sommerurlaub-2026_Detailcheck_Le-Torri_vs_La-Fenice]]. **Empfehlung: La Fenice + Casa Vacanze Sole.** **Nächster Schritt Tom:** La Fenice telefonisch klären (Casa-Verfügbarkeit, Tennis, Basketball im Ort), parallel Le Torri als Backup. Frist: Buchung bis Ende Juni.

## Erledigt (Kurzarchiv, letzte 5)

- ✅ 10.06. **Blitztext Grundinstallation:** App läuft, Diktat per Menüleisten-Klick + Auto-Paste funktioniert (Hotkeys → eigener Faden)

- **⏸️ dok-triage-mi-sa (pausiert 13.06.2026):** Scheduled Task deaktiviert — ordnerstruktur.md kollidiert mit Master-Plan v2 (kein Verein/gGmbH-Split, iCloud ≠ OneDrive für Praxis/SüdpfalzDOCs). **Reaktivieren nach** Abschluss Faden „Organisation: 6-Hüte-Setup": ordnerstruktur.md anpassen → Task in Cowork wieder einschalten.

### 🟢 Social Media: Positionierung + Content-Produktion (Kurs Sven)
- **Hut:** übergreifend / Personal Brand · **Stand:** 13.06. — Workbook ausgefüllt, 3 Content-Säulen definiert, favorisierte Instagram-Bio bestätigt, beide Canva-Template-Sets gesichtet (B-Roll 8 Slides + Karussell 12 Slides), Template-Mapping in Memory gespeichert.
- **Nächster Schritt:** (1) Eigene Fotos in Projektordner laden → Template-Matching · (2) 2–3 B-Roll-Videos (7 Sek.) erstellen — Slides 6/7 (schwarz+Text) sofort ohne Footage möglich · (3) erste Posts texten
- **Quellen:** [[2026-06-13-Social-Media-Positionierung]] · Memory `positionierung-social-media` + `instagram-content-system` · Projektordner `~/Documents/Claude/Projects/Kurs Sven Positionierung, KI, Instagram, etc., pp.`
