---
typ: regelwerk
erstellt: 2026-06-10
aktualisiert: 2026-06-10
---
# 📜 Verbindliche Regeln für alle Claude-Sessions

Gilt für **jede** Claude-Session (Claude Code, Claude Desktop, Cowork). Diese Datei ist die **einzige** Quelle für app-übergreifende Regeln — Regeln nie woanders duplizieren, nur hierher verweisen.

## Kanonische Quellen (bei Widerspruch gilt diese Rangfolge)

1. **Diese Datei** — app-übergreifende Regeln
2. **`~/Desktop/Claude /Projekte/Organisation/Master-Plan_Setup_2026-05.md`** — Soll-Zustand des Ordnungssystems (6 Hüte v2)
3. **`00_Faeden.md`** (dieser Vault) — aktueller Stand + nächster Schritt aller Projekte
4. **`99_Meta/Mail-System.md`** — Mail-Detailsystem
5. Claude-Code-Memory und App-Projektwissen sind **nur Verweise/Snapshots** — nie als eigenständige Wahrheit behandeln

## Änderungsprotokoll (Pflicht bei jeder Änderung an Ordnungssystemen)

Ordnungssysteme = Mail (Smart Mailboxen/Regeln), Kalender, Erinnerungen, Dateistrukturen, Master-Plan, Vault-Struktur.

1. **Vorher Ist-Zustand lesen** (App/Plist/kanonische Notiz) — nie blind anlegen
2. **Existiert es schon?** → erweitern oder ersetzen statt parallel neu anlegen (sonst Duplikate wie am 10.06.2026 bereinigt)
3. **Nachher im selben Zug:** Master-Plan-Datei UND zugehörigen Faden in `00_Faeden.md` aktualisieren
4. **Nichts löschen ohne Rückfrage** + Undo-Log/Backup anlegen
5. **Widerspruch zwischen Quellen entdeckt?** → nicht still weiterarbeiten, sondern Tom melden und in der kanonischen Quelle auflösen

## Bekannte Fallen (verifiziert, nicht „fixen")

- Apple Mail FlaggedStatus: **0 = Rot, 1 = Orange** — die Werte in den GTD-Mailboxen sind korrekt
- AppleScript-Klasse „smart mailbox" defekt (Fehler -2741) → Plist direkt schreiben, Mail vorher beenden
- Kalenderfarben nur als RGB-Liste {R,G,B} setzen — benannte Konstanten scheitern lautlos
- Obsidian-MCP `recent_changes` defekt
