---
date: 2026-06-07
thema: Smart Mailbox Sortierung prüfen
status: ERLEDIGT 10.06. — Achtung, FlaggedStatus-Analyse war FALSCH (siehe Korrektur unten)
tags: [mail, organisation, claude-session]
---

> ⚠️ **KORREKTUR 10.06.2026:** Die FlaggedStatus-Tabelle unten ist **falsch**. Apples Flaggen-Index ist `0 = Rot, 1 = Orange, 2 = Gelb …` (−1 = keine Flagge). Die bestehenden Werte (Follow-up rot = 0, Warten orange = 1) waren von Anfang an **korrekt** — Beleg: „Follow-up rot" zeigt 361 Treffer, bei „0 = nicht markiert" wären es zigtausend. **Die offenen Fixes „rot=1 / orange=2" NICHT ausführen** — sie würden das funktionierende System kaputtmachen. Duplikate „Teampraxis" + „⭐ To-Do (heute)" am 10.06. gelöscht (9 Boxen verbleiben). Details: [[2026-06-10-Konsistenz-Audit-Claude-Umgebung]]

## Zusammenfassung

Vollständige Bestandsaufnahme der Apple Mail Smart Mailboxen via Plist-Analyse.

## Ergebnis

**12 Mailboxen** gefunden (geplant waren 6 nach 6-Hüte-Plan v2):

| Name | Kriterium | Status |
|---|---|---|
| 📅 Heute | Datum = heute | ✅ OK |
| 📥 Praxis Bellheim | Konto schmitz@teampraxis-bellheim.de | ✅ OK |
| Verein | Exchange EWS-Konto | ⚠️ kein Emoji |
| 📥 Privat | Gmail + iCloud | ✅ OK |
| Berufliches & CME | Absender KV/KBV/Ärztekammer + Betreff | ✅ OK |
| ⭐ To-Do (heute) | Markiert + Ungelesen + VIP + Priorität | ✅ OK |
| Firma & Investments | Exchange + Betreff „gGmbH" | ⚠️ Duplikat zu gGmbH? |
| gGmbH | Exchange + Betreff „gGmbH" | ⚠️ Duplikat |
| Follow-up rot | FlaggedStatus = 0 | ❌ FEHLER: 0 = nicht markiert |
| Warten auf Antwort orange | FlaggedStatus = 1 | ❌ FEHLER: 1 = rot, nicht orange |
| Teampraxis | Absender @teampraxis-bellheim.de | ⚠️ Duplikat zu Praxis Bellheim? |

## Korrekte FlaggedStatus-Werte (Apple Mail)

| Farbe | FlaggedStatus |
|---|---|
| Rot | 1 |
| Orange | 2 |
| Gelb | 3 |
| Grün | 4 |
| Blau | 5 |
| Violett | 6 |

## Offene Fixes

- [ ] Follow-up rot: FlaggedStatus auf `1` setzen
- [ ] Warten auf Antwort orange: FlaggedStatus auf `2` setzen
- [ ] „Verein" umbenennen mit Emoji
- [ ] Duplikate prüfen: Firma & Investments vs. gGmbH, Teampraxis vs. Praxis Bellheim
- [ ] Entscheidung: 6 oder 12 Mailboxen gewünscht?

## Weiteres aus der Sitzung

- Neues Setup: Claude schreibt ab sofort nach jedem Chat Zusammenfassung → Memory + Obsidian (`99_Meta/Cowork-Chats/`)
