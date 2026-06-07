---
typ: cowork-chat
datum: 2026-06-05
thema: Apple Mail Smart-Mailboxen und Regeln
status: beobachten
---
# Cowork: Mail-System-Reorganisation (05.06.2026)

## Auftrag
1. Smart-Mailbox-Sortierung in Apple Mail prüfen (6 Hut-Mailboxen)
2. Folder-Konzept (`00 Privat`, `10 Praxis Bellheim` etc.) klären — funktioniert nicht wie geplant
3. Optimieren und schärfen

## Erkenntnisse / Fund

**Smart Mailboxen (Auswertung):**
- Praxis Bellheim (3.564), Verein (4.260), gGmbH (52) — sauber, Account-basiert
- Privat (57.050) — historisch ab 2010, plus Bug: leerer dritter Account-Filter
- Berufliches & CME (3.068) — leakt: Teampraxis-Forwards via Betreff `Fortbildung`, KV-Abrechnung via Absender `kv-rlp`
- Firma & Investments (953) — Sonocoach + Jackery bewusst drin, aber wahrscheinlich nicht mehr passend

**Folder-Struktur:** existiert komplett (`00 Privat`, `10 Praxis Bellheim`, `20 Berufliches & CME`, `30 Firma & Investments`, `40 SüdpfalzDOCs`, `90 Archiv` + `_FOLLOW_UP` / `_WARTEN_AUF_ANTWORT`) mit Themen-Unterordnern.

**Kern-Problem:** 17 Mail-Regeln existieren, **16 waren deaktiviert**. Nur „DMP – Abrechnung" war aktiv. Deshalb blieben die Ordner leer.

## Umgesetzt

| Änderung | Status |
|---|---|
| Privat-Smart-Mailbox: leerer Account-Filter entfernt | erledigt |
| Smart Mailbox „Follow-up rot" angelegt (rote Flag → 361 Treffer) | erledigt |
| Smart Mailbox „Warten auf Antwort orange" angelegt (orange Flag → 12 Treffer) | erledigt |
| Regel „CME & Fortbildung" reaktiviert (Pilot) | aktiv |
| Regel „Smartlaunch → Firma & Investments" reaktiviert | aktiv |
| Regel „Bay. Ärzteversorgung → Privat Finanzen" reaktiviert | aktiv |
| Regel „ING-DiBa → Privat Finanzen" reaktiviert | aktiv |
| Regel „SüdpfalzDOCs → 40 Ordner" — Zielordner kaputt | offen (manuell durch Tom) |

5 von 17 Regeln jetzt aktiv (vorher nur 1).

## Entscheidungen

- **GTD via Flag-Farben** statt manueller Ordner-Bewegung. Rot = Follow-up, Orange = Warten auf Antwort.
- **Lokale Folder-Struktur bleibt erhalten** (kein Datenverlust), Mails werden per Regel reinverschoben.
- **Eine Regel pro Session als Pilot**, dann Welle freischalten.
- **SüdpfalzDOCs-Ziel** = `40 SüdpfalzDOCs` (Root), Tom sortiert intern in die 4 Unterordner.

## Offen / Nächste Schritte

- [ ] SüdpfalzDOCs-Regel manuell reparieren (Duplikate raus, Ziel = `40 SüdpfalzDOCs`, aktivieren) 📅 2026-06-06
- [ ] 24-48h beobachten ob die 4 neu aktivierten Regeln sauber sortieren 📅 2026-06-07
- [ ] Bei sauberem Pilot: nächste Regelwelle aktivieren (Ärztekammer, PVS, KV-KVRLP, Honorarabrechnung, Krankenkassen, Sparkasse, Versicherungen, Steuer) 📅 2026-06-08
- [ ] Smart-Mailbox-Feinschliff: Berufliches & CME schärfen (`kv-rlp` raus, `Fortbildung` mit UND-NICHT Teampraxis); Firma & Investments — Sonocoach/Jackery klären

## Quellen

- [[99_Meta/Mail-System]] — komplette System-Doku
- Cowork-Output: `mail_gesamt_bilanz.md`
- Cowork-Output: `mail_undo_log.md` (Vorher-Stand pro Änderung)
