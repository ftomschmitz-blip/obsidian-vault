---
typ: cowork-chat
datum: 2026-06-10
thema: Konsistenz-Audit Claude-Umgebung (Code/Desktop/Cowork)
status: erledigt (Mailbox-Bereinigung offen)
tags: [organisation, claude, audit, master-plan]
---
# Cowork: Konsistenz-Audit Claude-Umgebung (10.06.2026)

## Auftrag

Tom: Claude-Umgebung auf sich gegenseitig beeinflussende/störende Regeln und Anweisungen prüfen — Ordnungssysteme (z. B. Master-Plan Setup) wurden aus Claude Code, Claude Desktop und Cowork parallel gestartet. Fehler korrigieren.

## Erkenntnisse / Fund (5 Konflikte)

1. **Master-Plan v1 vs. v2 (Kernkonflikt):** Planfile war auf v1 (4 Hüte, „Verein+gGmbH zusammen"), Memory/Faden auf v2 (6 Hüte, getrennt). Eine andere Session hat die Datei heute parallel teilmigriert — Roadmap-, Tasks-, Mailbox- und Dateien-Abschnitte enthielten aber weiter v1-Anweisungen (z. B. „4 Farb-Kalender Blau/Rot/Grün/Orange [Beschlossen]" direkt unter dem v2-Revisionsbanner).
2. **Smart Mailboxen doppelt (gegenseitige Störung bestätigt):** 11 Boxen in der Plist — v1-Generation (06.05., Claude Code: 📅 Heute, 📥 Privat, 📥 Praxis Bellheim, ⭐ To-Do) + v2-Generation (05.06., Cowork: Teampraxis, Berufliches & CME, Firma & Investments, Verein, gGmbH, Follow-up rot, Warten auf Antwort orange). Duplikate: 📥 Praxis Bellheim↔Teampraxis, ⭐ To-Do↔GTD-Flags.
3. **Erinnerungen-Wildwuchs:** 4 v1-Hut-Listen (🔵🔴🟢🟠) + 8 Alt-Listen, „Erinnerungen Private" doppelt. v2 (6 Listen) nie umgesetzt.
4. **Regelkonflikt Arbeitsbereich:** `Projekte/CLAUDE.md` verbot Dateien außerhalb von `Desktop/Claude /` — widersprach dem Session-Ritual (Obsidian-Vault schreiben) und den Cowork-Projektordnern.
5. **Leere `~/CLAUDE.md`** (0 Bytes) im Home — Überbleibsel, gelöscht.

## Umgesetzt

- **Master-Plan-Datei** vollständig auf v2 konsolidiert: Roadmap Woche 2 (6 Farb-Kalender, Verein/gGmbH getrennt), Woche 3 (6 Listen), Woche 5 (Cheat-Sheet 6 Hüte), Tasks-/Mailbox-/Dateien-Abschnitte mit Ist-Zustand 10.06.; Kanonische-Quellen-Regel ergänzt.
- **Anti-Drift-Regel etabliert:** Planfile = Soll · `00_Faeden.md` = Stand · Claude-Code-Memory = nur Verweis. Jede Session, die das Setup ändert, aktualisiert Planfile UND Faden.
- **Memory** `project_organisation_setup.md` neu geschrieben (keine Plan-Kopie mehr), MEMORY.md-Index angepasst.
- **`Projekte/CLAUDE.md`:** Ausnahmen ergänzt (Obsidian-Vault, Memory, Cowork-Ordner, Systemkonfiguration mit Undo-Log).
- **Fäden** „Organisation" + „Mail-System" in `00_Faeden.md` mit Befund aktualisiert.
- Leere `~/CLAUDE.md` gelöscht.

## Entscheidungen

- Keine Eingriffe in Apple-Apps in dieser Session (goldene Regel: nichts löschen ohne Rückfrage). Mailbox-Bereinigung, FlaggedStatus-Fix, Erinnerungen-Migration → Woche-2-Wiederholung bzw. nach Toms Entscheidung.

## Offen / Nächste Schritte

- [ ] Tom entscheidet: v1-Mailbox-Reste löschen (📥 Praxis Bellheim, ⭐ To-Do (heute); 📥 Privat/📅 Heute klären)? 📅 2026-06-14
- [ ] Woche 2 wiederholen: 6 v2-Kalenderfarben + Erinnerungen-Migration + Mailbox-Bereinigung in einem Zug
- [ ] Erinnerungen: Alt-Listen konsolidieren („Erinnerungen Private" doppelt)

## Quellen

- `~/Desktop/Claude /Projekte/Organisation/Master-Plan_Setup_2026-05.md` (konsolidiert)
- [[Mail-System]] · [[2026-06-07-Smart-Mailbox-Sortierung]] · [[00_Faeden]]
