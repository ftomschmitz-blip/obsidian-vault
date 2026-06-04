---
typ: anleitung
erstellt: 2026-06-04
---
# 🛠️ System-Anleitung – Second Brain

Schlankes Arbeitssystem: **ein Eingang zum Erfassen, ein Ort für alles Offene.**

## Die 3 Bausteine
1. **Tagesnotiz** (`999_Tagesnotizen/`): dein täglicher Startpunkt. Inbox, Aufgaben, Termine, Log.
2. **Cockpit** (`00_Cockpit.md`): zieht automatisch alle offenen Aufgaben aus dem ganzen Vault zusammen, gruppiert nach Rolle/Ordner.
3. **Vorlagen** (`99_Meta/Vorlagen/`): Tagesnotiz + Meeting.

## Plugins (einmalig installieren)
Einstellungen → Community-Plugins → Durchsuchen → installieren **und aktivieren**:
- **Dataview** (Listen/Abfragen)
- **Tasks** (Aufgaben mit Fälligkeit)
- **Templater** (Vorlagen mit Datum)

Alle drei lokal, kostenlos, kein Cloud-Zugriff.

## Konfiguration (einmalig)
**Core → Tägliche Notizen:**
- Neue-Datei-Speicherort / Ordner: `999_Tagesnotizen`
- Vorlagendatei-Speicherort: `99_Meta/Vorlagen/Tagesnotiz`

**Templater (Einstellungen → Templater):**
- Template folder location: `99_Meta/Vorlagen`
- „Trigger Templater on new file creation": **AN** (damit `<% %>` in neuen Tagesnotizen automatisch ersetzt wird)
- Optional unter „Folder Templates": Ordner `999_Tagesnotizen` → Vorlage `99_Meta/Vorlagen/Tagesnotiz`

**Tasks (Einstellungen → Tasks):**
- Globaler Filter optional leer lassen (alle `- [ ]` zählen als Aufgaben).
- Datumsformat: Standard belassen.

## Täglicher Ablauf
1. Morgens **Tagesnotiz** öffnen (Core: „Tägliche Notiz öffnen", oder Hotkey).
2. Alles Reinkommende in die **Inbox** der Tagesnotiz werfen.
3. Aufgaben als `- [ ] …` notieren, Fälligkeit über das Tasks-Kommando setzen.
4. Bei Bedarf **Cockpit** öffnen → Überblick über alle Rollen.
5. Wochenende: Cockpit durchgehen, Erledigtes abhaken, Offenes neu terminieren.

## Aufgaben-Schnellsyntax (Tasks)
- `- [ ] Aufgabe 📅 2026-06-10` → fällig am 10.06.
- `- [ ] Aufgabe ⏫` → hohe Priorität (🔼 mittel, 🔽 niedrig)
- `- [ ] Aufgabe 🔁 every week` → wiederkehrend
- Komfortabel über Kommando-Palette: **„Tasks: Create or edit task".**

> Hinweis: Aufgaben können in *jeder* Notiz stehen (Projekt, Praxis, Privat …) – das Cockpit sammelt sie automatisch nach Ordner/Rolle.
