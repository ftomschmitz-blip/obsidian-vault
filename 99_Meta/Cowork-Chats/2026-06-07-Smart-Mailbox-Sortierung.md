---
date: 2026-06-07
thema: Smart Mailbox Sortierung prüfen
status: Analyse abgeschlossen – Fixes ausstehend
tags: [mail, organisation, claude-session]
---

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
