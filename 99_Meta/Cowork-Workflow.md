---
typ: anleitung
erstellt: 2026-06-05
thema: cowork-routine
---
# 🤝 Cowork-Workflow

## Stehende Regel: Chat-Zusammenfassung nach jeder Session

**Jede Cowork-Session endet mit:**

1. **Kompakte Zusammenfassung** des Chats (was besprochen, was entschieden, was umgesetzt, was offen).
2. **Speichern in Obsidian** unter `99_Meta/Cowork-Chats/YYYY-MM-DD-Kurztitel.md`.
3. **Verlinken** aus der Tagesnotiz (`999_Tagesnotizen/YYYY-MM-DD.md`) unter dem Log-Abschnitt.
4. **Offene Aufgaben** als Tasks mit Fälligkeit in die Tagesnotiz, damit sie im Cockpit landen.
5. **Faden-Update** in `00_Faeden.md`: den zugehörigen Block aktualisieren (Stand + Nächster Schritt). Neues Vorhaben? → in den **Parkplatz**, nicht zu den aktiven Fäden (WIP-Limit 7; Aktivierung nur im Wochenreview).

## Format der Zusammenfassungs-Datei

```markdown
---
typ: cowork-chat
datum: YYYY-MM-DD
thema: Kurztitel
status: erledigt | beobachten | offen
---
# Cowork: Kurztitel (Datum)

## Auftrag
Was wollte Tom?

## Erkenntnisse / Fund
Was wurde festgestellt?

## Umgesetzt
Konkrete Änderungen, am besten mit Vorher/Nachher.

## Entscheidungen
Welche Optionen besprochen, welche Auswahl getroffen?

## Offen / Nächste Schritte
Tasks mit Fälligkeit.

## Quellen
Links zu Dateien in Cowork-Outputs, andere Obsidian-Notizen.
```

## Wozu

- Cowork hat keine Memory zwischen Sessions — Obsidian ist Toms persistenter Speicher.
- Beim nächsten Mal kann Tom die Notiz öffnen oder Claude bitten, sie zu lesen → sofort wieder im Bild.
- Tasks landen automatisch im Cockpit.

## Claude-App-Projekte: Sync-Regel

**Der Vault ist die Wahrheit, Projektwissen ist nur ein Snapshot.** Dateien im Projektwissen der Claude-App können nicht automatisch aktualisiert werden — bei Bedarf manuell neu hochladen (Drag & Drop).

**Diesen Text in die Projekt-Instruktionen jedes Claude-App-Projekts einfügen (Stand 10.06.2026, ersetzt ältere Fassung):**

> Zu Session-Beginn: `00_Regeln.md` (verbindliche app-übergreifende Regeln) und bei laufenden Themen `00_Faeden.md` via mcp-obsidian lesen. Vor jeder Änderung an Ordnungssystemen (Mail, Kalender, Erinnerungen, Dateistrukturen, Master-Plan): erst Ist-Zustand lesen, Bestehendes erweitern statt parallel neu anlegen, nichts löschen ohne Rückfrage. Am Ende jeder Session: (1) Zusammenfassung nach `99_Meta/Cowork-Chats/YYYY-MM-DD-Kurztitel.md` schreiben, (2) in `00_Faeden.md` den zugehörigen Faden-Block aktualisieren (Stand + Nächster Schritt), (3) bei Setup-Änderungen zusätzlich die Master-Plan-Datei (`~/Desktop/Claude /Projekte/Organisation/Master-Plan_Setup_2026-05.md`) nachführen.

## Wochenreview (freitags oder sonntags, 15 Min)

Tom startet in irgendeiner Claude-Session mit „Wochenreview bitte". Ablauf:
1. `00_Faeden.md` lesen und jeden aktiven Faden durchgehen: Was ist passiert? Stockt etwas? Erledigt?
2. **Konsistenz-Check (2 Min):** Stimmen Master-Plan-Datei, `00_Faeden.md` und Claude-Code-Memory überein? Widersprechen sich Regeln in `00_Regeln.md`, CLAUDE.md-Dateien oder Projekt-Instruktionen? Drift sofort in der kanonischen Quelle auflösen (Rangfolge in `00_Regeln.md`).
3. Parkplatz sichten: Was wird aktiviert (nur wenn < 7 aktive Fäden)?
4. **Top-3 der Woche** neu setzen — gemeinsam, Tom entscheidet.
5. Erledigtes ins Kurzarchiv verschieben, `aktualisiert:`-Datum setzen.

## Sonderfall: rein konversationelle Chats

Wenn ein Chat nur Kurz-Auskunft war (Fakten-Frage, kein Tool-Einsatz, keine Datei-Erzeugung), reicht ein einzeiliger Vermerk in der Tagesnotiz. Keine eigene Zusammenfassungs-Datei nötig.
