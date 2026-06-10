---
date: 2026-06-10
thema: Blitztext Hotkeys debuggen
status: offen
tags: [blitztext, macos, diktat]
---

# Blitztext: Hotkeys funktionieren nicht (Session-Protokoll)

## Zusammenfassung
Blitztext läuft und diktiert zuverlässig, wenn man die Aufnahme per Menüleisten-Klick startet (Auto-Paste funktioniert — Diktate landeten im Chat). Die Hotkeys reagierten aber nicht. Systematische Fehlersuche im Quellcode.

## Ergebnisse
1. **Falsche Hotkey-Belegung notiert:** Laut `HotkeyService.swift` macht `fn` allein **nichts**. Korrekte Belegung:
   - `fn + Shift` = Transkription
   - `fn + Control` = Blitztext+ (Textverbesserer)
   - `fn + Option` = Dampf ablassen
   - `fn + Command` = Emojis
   - `fn + Shift + Control` = lokale Transkription
2. **`AppleFnUsageType` stand wieder auf 3** (Apple-Diktat) — erneut auf 0 („Nichts tun") gesetzt. Wert scheint zurückzudriften, bei fn-Problemen zuerst prüfen: `defaults read com.apple.HIToolbox AppleFnUsageType`
3. Whisper-Artefakte beobachtet: „[Anhaltender Beifall]" bei Stille am Ende, „Clodesk Top"/„Glut Desktop" für „Claude Desktop".

## Offene Punkte
- [ ] Test: `fn + Shift` halten → sprechen → loslassen
- [ ] Falls tot: Bedienungshilfen-Berechtigung prüfen (alte Blitztext-Einträge entfernen, nur aktuellen Build freigeben, App neu starten) — globaler Tastatur-Monitor braucht diese Berechtigung
- [ ] Für Patientendaten: „Sicherer Lokaler Modus" mit WhisperKit-Modell einrichten (noch nicht installiert)

## Kontext für Folge-Session
Arbeitsverzeichnis: `/Users/tschmitz` · Repo: `~/blitztext-app` · Memory: `project_blitztext.md` ist aktuell.
