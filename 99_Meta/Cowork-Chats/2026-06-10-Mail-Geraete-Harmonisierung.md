---
typ: session-log
erstellt: 2026-06-10
thema: apple-mail, geraete-sync
---
# Mail-Harmonisierung über alle Geräte (Cowork-Session)

## Ausgangsfrage
Tom wollte Mail-Ordner, intelligente Postfächer und Konten-Aufbau über iPhone/iPad/Mac harmonisieren.

## Vorgehen
Nur-Lese-Analyse von `~/Library/Mail/V10` (Festplattenvollzugriff von Tom erteilt, Ordner in Session gemountet). Keine Änderungen an Mail vorgenommen.

## Befunde
- **Drift zu [[Mail-System]]:** Die Notiz behauptet, Regeln verschieben in lokale Ordner. Tatsächlich zielen 7 von 8 aktiven Regeln auf **iCloud-Server-Ordner**; die Struktur 00–90 existiert bereits serverseitig (inkl. `_FOLLOW_UP`/`_WARTEN_AUF_ANTWORT`).
- Einzige lokale Ausnahme: Regel „SüdpfalzDOCs → 40 Ordner" (`local:///40 SüdpfalzDOCs`).
- Lokaler Restbestand: 40 SüdpfalzDOCs **3.462 Mails / 3,8 GB**, 10 Praxis **93 Mails / 115 MB**, übrige lokale Ordner leer.
- **⚠️ Anomalie: lokaler Postausgang enthält 129 Mails / 770 MB** — möglicherweise nie versendet. Prüfen!
- iCloud-Plan 2 TB → Speicher kein Hindernis.
- Apple-Grenzen bestätigt: Smart Mailboxes existieren auf iOS nicht; lokale Ordner sind mobil unsichtbar; Flags syncen überall.

## Ergebnis
Entscheidungsvorlage erstellt (Cowork-Outputs: `Entscheidungsvorlage_Mail-Harmonisierung_2026-06-10.md`). Empfehlung: Weg A fertigstellen — Server-Ordner für 40 anlegen (oder Exchange-Konto direkt), Regel umstellen, 3,9 GB Bestand umziehen, TEST_ICLOUD_FOLDER löschen. Vorher Outbox klären; Time-Machine-Stand vor dem Umzug.

## Offen
- Tom entscheidet: 40er-Ziel auf iCloud oder ins Exchange-Konto SüdpfalzDOCs
- Nach Umsetzung: [[Mail-System]] korrigieren (Regel-Ziele, lokale Ordner)

## Nachtrag (gleiche Session): Outbox-Anomalie geklärt
Forensischer Abgleich der 129 Outbox-Dateien gegen den Envelope Index (read-only, immutable): Postausgang laut Index **leer** (daher in Mail-UI unsichtbar) → verwaiste Arbeitskopien. **126/129 in „Gesendet" nachgewiesen** (Abgleich Betreff ohne Re:/Fwd:-Präfix ± 3 Tage). Boarding Pass: Zustellung an eigenen Posteingang belegt. Offen nur: „Fwd: Vorhaltepauschale 2026" an C. Weißler (24.03.2026, wahrscheinlich versendet — Tom fragt nach oder sendet erneut) und „Präsentation Sommerakademie" (07/2024, irrelevant). Verwaiste Dateien können beim Aufräumschritt entfernt werden (nur nach Rückfrage).
