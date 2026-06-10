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

---

## Nachtrag (gleiche Session, später): Mailbox-Bereinigung durchgeführt

- **Gelöscht** (von Tom bestätigt): „Teampraxis" + „⭐ To-Do (heute)" → 9 Smart Mailboxen verbleiben. Backup: `~/Desktop/Claude /Projekte/Organisation/SyncedSmartMailboxes_BACKUP_2026-06-10.plist`
- **Wichtige Korrektur der Korrektur:** Die 07.06.-Analyse hatte die Lösch-Empfehlung falsch herum („📥 Praxis Bellheim" weg) und einen falschen FlaggedStatus-Fix (rot=1/orange=2) notiert. Tatsächlich: „📥 Praxis Bellheim" (Konto-Filter) ist die bessere, dokumentierte Box; FlaggedStatus 0=Rot/1=Orange ist Apples korrekter Index — die Werte stimmten von Anfang an. Der falsche „Fix" hätte den GTD-Workflow zerstört. Notiz vom 07.06. mit Warnbanner korrigiert.
- Mail wurde für den Plist-Eingriff beendet und danach neu gestartet.
- **Offen:** Einige Tage beobachten, ob der iCloud-Sync die 9 Boxen stabil hält.

---

## Nachtrag 2: Drift-Prävention eingerichtet

Auftrag: künftige Regel-Konflikte zwischen den Apps strukturell verhindern.

1. **`00_Regeln.md`** (Vault-Root) neu angelegt — einzige Quelle für app-übergreifende Regeln: Rangfolge der kanonischen Quellen, Änderungsprotokoll für Ordnungssysteme (Ist-Zustand lesen → erweitern statt neu → Plan+Faden nachführen → nichts löschen ohne Rückfrage → Widersprüche melden), bekannte Fallen (FlaggedStatus, AppleScript-Bugs).
2. **SessionStart-Hook** in `~/.claude/settings.json`: lädt `00_Regeln.md` automatisch in jede Claude-Code-Session (greift ab der nächsten Session).
3. **`~/.claude/CLAUDE.md`**: Kurzverweis auf `00_Regeln.md` ergänzt (Absicherung, falls Hook nicht greift).
4. **`99_Meta/Cowork-Workflow.md`**: Paste-Block für Projekt-Instruktionen erweitert (Regeln lesen, Ist-Zustand prüfen, Master-Plan nachführen); Wochenreview um 2-Min-Konsistenz-Check ergänzt (neuer Schritt 2).
5. **Memory**: neuer Eintrag `feedback_zentrale_regeln.md`.

**[Tom] Einmalig (5 Min):** Den aktualisierten Paste-Block aus `Cowork-Workflow.md` in die Projekt-Instruktionen der bestehenden Claude-App-Projekte einfügen (Cowork/Desktop: Projekt → Instruktionen) und sinngemäß in die persönlichen Präferenzen der Claude-App (Einstellungen → Profil), damit auch projektlose Desktop-Chats die Regel kennen.
