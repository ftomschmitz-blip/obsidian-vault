---
typ: anleitung
erstellt: 2026-06-05
thema: apple-mail
---
# 📬 Apple Mail — Smart Mailboxen + Regeln

Schlankes Mail-System: **Hut-Sichten als Smart Mailboxen + automatische Vorsortierung in lokale Ordner.**

## Die 3 Bausteine

1. **Smart Mailboxen** (Hut-Sichten) — filtern alle Konten/Ordner durch, keine echte Bewegung.
2. **Lokale Ordner** „Auf meinem Mac" — Archivablage mit Themen-Unterordnern (00–90).
3. **Mail-Regeln** — verschieben eingehende Mails automatisch in die richtigen lokalen Ordner.

## Smart Mailboxen (Stand 2026-06-05)

| Sicht | Filter | Treffer | Bewertung |
|---|---|---|---|
| Praxis Bellheim | Account = Teampraxis-Bellheim | 3.564 | sauber |
| Berufliches & CME | Absender/Betreff CME-Trigger | 3.068 | leakt Teampraxis + KV-Abrechnung |
| Firma & Investments | Absender smartlaunch · lazy-investors · sonocoach · jackery | 953 | bewusst, Sonocoach/Jackery prüfen |
| Privat | Account iCloud + tomschmitz@me.com | 57.050 | historisch ab 2010 |
| Verein | Account = t.schmitz@suedpfdoc.de | 4.260 | sauber |
| gGmbH | Account Verein + Betreff "gGmbH" | 52 | eigene Domain fehlt noch |
| Follow-up rot | E-Mail markiert = Rot | 361 | GTD-Workflow |
| Warten auf Antwort orange | E-Mail markiert = Orange | 12 | GTD-Workflow |

## GTD-Markierung

- **Rote Flag** → Mail erscheint in „Follow-up rot", muss bearbeitet werden
- **Orange Flag** → Mail erscheint in „Warten auf Antwort orange", warte auf Antwort
- Flag entfernen wenn erledigt

## Aktive Regeln (Stand 2026-06-05)

| Regel | Filter | Ziel |
|---|---|---|
| DMP – Abrechnung | (Krankenkassen-Trigger) | 10 Praxis Bellheim → HZV & DMP |
| CME & Fortbildung | cme-verlag · elearning · Fortbildungspunkte · CME-Punkte | 20 Berufliches & CME → Fortbildung & CME |
| Smartlaunch | smartlaunch · lazy-investors | 30 Firma & Investments → Smartlaunch |
| Bay. Ärzteversorgung | bayerische-aerzteversorgung · bav.de | 00 Privat → Finanzen & Versicherungen |
| ING-DiBa | ing-diba.de · ing.de | 00 Privat → Finanzen & Versicherungen |

## Deaktivierte Regeln (12 — warten auf Pilotbeobachtung)

- SüdpfalzDOCs → 40 Ordner (Zielordner muss erst gesetzt werden)
- Neuigkeiten von Apple
- KV KVRLP → Praxis Abrechnung
- PVS → Praxis Abrechnung
- Honorarabrechnung → Praxis Abrechnung
- Krankenkassen → Praxis HZV & DMP
- Bewerbungen → Praxis Personal
- Sparkasse → Praxis Lieferanten
- Ärztekammer → Berufliches
- Versicherungen → Privat Finanzen
- Rechnungen an Praxis-Adresse → Lieferanten
- Steuer & Finanzamt → Privat Finanzen

## Ordnerstruktur „Auf meinem Mac"

```
_FOLLOW_UP                   (manuelle GTD-Ablage)
_WARTEN_AUF_ANTWORT          (manuelle GTD-Ablage)
00 Privat                    → Familie · Finanzen & Versicherungen · Gesundheit · Reisen & Freizeit · Wohnen
10 Praxis Bellheim           → Abrechnung & KV · Behörden · HZV & DMP · Kollegen & Ärzte · Lieferanten & Rechnungen · Personal & MFA
20 Berufliches & CME         → Fortbildung & CME (+ weitere)
30 Firma & Investments       → Smartlaunch (+ weitere)
40 SüdpfalzDOCs              → Behörden & KV · Dienstplanung · Finanzen SüdpfalzDOCs · Mitglieder
90 Archiv
```

## Workflow

1. Mail kommt rein → aktive Regel verschiebt sie ggf. in lokalen Ordner
2. Du flaggst sie nach Bedarf rot (Follow-up) oder orange (Warten auf Antwort)
3. Smart Mailbox zeigt sie als Sicht (egal in welchem Ordner sie liegt)
4. Erledigt → Flag entfernen oder von Hand in Unter-Archiv schieben

## Offen / Beobachten

- 24–48 h nach 2026-06-05: prüfen ob die neuen Regeln sauber sortieren
- SüdpfalzDOCs-Regel manuell reparieren: Duplikate raus + Ziel auf `40 SüdpfalzDOCs`
- Bei sauberem Pilot: nächste Regelwelle (Ärztekammer, PVS, KV-KVRLP, Honorarabrechnung, Krankenkassen, Sparkasse usw.)
- Smart-Mailbox-Feinschliff: Berufliches & CME schärfen (`kv-rlp` raus, `Fortbildung` mit UND-NICHT)

## Quellen

- Vollständige Gesamt-Bilanz: `outputs/mail_gesamt_bilanz.md` (Cowork-Session)
- Undo-Log mit Vorher-Stand pro Änderung: `outputs/mail_undo_log.md` (Cowork-Session)
