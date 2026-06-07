---
typ: anleitung
erstellt: 2026-06-07
thema: effektive-nutzung
---
# 📘 Effektiv-Nutzung – So arbeitest du im System

> Ergänzt [[System-Anleitung]] (Grundlagen) um die **tägliche Praxis** mit Dashboard, Projekten, Dokumenten und Review.
> Faustregel: **Erfassen → Klären → Ablegen → Wiedervorlegen.** Nie im Kopf behalten, was eine Notiz halten kann.

---
## ⏱️ Täglicher Ablauf (ca. 5 Min)

1. **Tagesnotiz öffnen** (Hotkey „Tägliche Notiz öffnen"). Das ist dein einziger Eingang.
2. **Reinwerfen:** Alles Neue (Mail, Anruf, Idee, Brief) unsortiert in die **Inbox** der Tagesnotiz.
3. **Aufgaben markieren:** Was zu tun ist, als `- [ ] …` schreiben, Fälligkeit per Kommando „Tasks: Create or edit task" setzen.
4. **Klären (1 Frage pro Zeile):** Gehört das zu einem Projekt? → in die Projekt-Notiz verschieben. Ist es ein wichtiges Dokument? → Dokument-Notiz anlegen. Sonst: erledigen oder terminieren.
5. **Cockpit kurz prüfen** ([[00_Cockpit]]): Was ist heute/überfällig?

---
## 📅 Wochen-Review (ca. 15 Min, z. B. Freitag)

1. **[[00_Cockpit]] öffnen** → „Überfällig" abarbeiten oder neu terminieren (nichts unkommentiert liegen lassen).
2. **Bereichs-Dashboard öffnen** (z. B. [[_Dashboard]] für SüdpfalzDOCs) → laufende Projekte durchgehen: Hat jedes einen **nächsten Schritt** mit Datum?
3. **Erledigtes abhaken** (`- [x]`), abgeschlossene Projekte auf `status: abgeschlossen` setzen.
4. **Dokumente mit Frist** prüfen → fristnahe Punkte als Aufgabe terminieren.
5. **Inbox leeren:** offene Inbox-Zeilen der Woche einsortieren.

---
## ➕ Wie lege ich etwas an?

### Neues Projekt
> Ordner `…/Projekte/` → neue Notiz → Vorlage **Projekt** anwenden (Templater: „Insert template").
- Ziel in einem Satz, **Deadline** + **nächster Schritt mit Datum** ausfüllen.
- Taucht automatisch im Dashboard & im Projekt-Index auf.

### Neues Dokument (wichtige Post/Vertrag/Bescheid)
> Ordner `…/Dokumente/` → Vorlage **Dokument**. Dateiname: `JJJJ-MM-TT_Absender_Thema`.
- **PDF/Scan bleibt in der iCloud-Ablage** — hier nur Pfad/Link + Metadaten (Frist!).
- Nur für Dokumente, die du **wiederfinden** oder deren **Frist** du verfolgen musst. Nicht jedes PDF.

### Neue Sitzung / Meeting
> Ordner `…/Sitzungen/` → Vorlage **Meeting**. Action Items als `- [ ]` mit Fälligkeit → landen automatisch im Dashboard.

---
## 🔎 Wo schaue ich?

| Frage | Ort |
|---|---|
| Was ist insgesamt zu tun? | [[00_Cockpit]] (alle Rollen) |
| Was läuft in *einem* Bereich? | Bereichs-`_Dashboard` |
| Welche Projekte gibt es? | `Projekte/_… (MOC)` |
| Wo liegt Dokument X / welche Frist? | `Dokumente/_… (MOC)` |
| Was wurde in Sitzung Y beschlossen? | `Sitzungen/_… (MOC)` |

---
## 🤖 Automatischer Morgen-Briefing

Werktags morgens fasst ein geplanter Cowork-Task deine **überfälligen + heute/3-Tage-fälligen** Aufgaben zusammen und schickt sie dir.
**Voraussetzung:** Mac an, Obsidian offen, Cowork-App läuft. Sonst entfällt der Lauf — die dokumentierte Routine oben greift dann manuell.

---
## 🧱 Muster auf andere Bereiche ausrollen

Das SüdpfalzDOCs-Gerüst (Dashboard + Projekte/Dokumente/Sitzungen mit Index) ist eine **Blaupause**. Für Praxis Bellheim oder Firma & Investments: gleiche Struktur kopieren, in den Queries nur den Ordnerpfad tauschen. Claude kann das auf Zuruf anlegen.
