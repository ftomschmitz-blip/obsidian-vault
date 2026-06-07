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

## Sonderfall: rein konversationelle Chats

Wenn ein Chat nur Kurz-Auskunft war (Fakten-Frage, kein Tool-Einsatz, keine Datei-Erzeugung), reicht ein einzeiliger Vermerk in der Tagesnotiz. Keine eigene Zusammenfassungs-Datei nötig.
