---
typ: cowork-chat
datum: 2026-06-12
projekt: Praxis Assistent zur Datenanalyse KV Abrechnungen
---
# KV-Pipeline rekonstruiert + Datensatz 12.06. verarbeitet

## Was passiert ist
- `kv_bellheim.py` war mit den alten Session-Outputs verloren → aus den dokumentierten Parser-Ankern **rekonstruiert** und gegen echte Daten getestet (Selftest 6/6).
- **Verbesserung:** GOP-/Vergütungsgruppen-Tabelle im CON wird jetzt exakt via pdfplumber-x-Koordinaten geparst → **100,0 % Honorar-Erfassung** (vorher heuristisch ~92,8 %). Kontrolle: LANR-Summen = Seite-1-Werte (±0,04 € KV-Rundung).
- Neuer KV-Datensatz **Z01510119500_12.06.2026_15.44** aus Downloads_Cloud verarbeitet (Ordner per Cowork direkt eingebunden, kein manuelles Kopieren).
- PDFs + tomedo-Exporte (KV + EBM, 12.06.) in den Projektordner kopiert (`KV-PDFs/`, `tomedo-Exporte/`); Quelle unangetastet.
- Neu: **Snapshot-JSON je Datensatz** (`snapshots/`) → Dashboard zeigt automatisch Δ zum Vorlauf; Baseline 06.06. aus Handover-Werten geseedet.

## Kennzahlen 12.06. (vs. 06.06.)
- Honorar **209.326,50 €** (+12.951,50) · Fallwert **86,46 €** (+1,49) · Fälle 2.421 (+110) · Scheine 2.424 (+108)
- Leydecker 59.338,30 € · Leske 96.332,13 € · Schmitz 53.656,04 €
- Vorhaltepauschale 8/10 → Zuschlag 03042 · TI voll · KBV-Prüfmodul OK
- Vorprüfung: 50 Treffer — Sofort 4 / Diese Woche 6 / Info Q3 40 (DMP Trier)
- **Honorarwirksame Treffer 38 → 10** (Korrekturen der Vorwoche haben gegriffen)

## Offene Punkte (Frist 30.06.)
1. 3 SKT-Scheine: Abdule, Bülbül, **neu Al Humsi**
2. Fall Ruppender zurückgestellt (kurative Diagnose fehlt, 89102A, Leske)
3. 6 GOP-Konflikte: 02300 (2×, Bülbül), 02310 (Stenner), 03062 (Lorenz), 03230 (Weber, Stober)
4. **Kriterium 10 Sprechstundenzeiten weiterhin „Nein"** (Mitgliederbereichs-Fix nicht umgesetzt!) · Video 0,59 % (Ziel ≥1 %, fehlen ca. 10–11 Videofälle — Einschätzung) → Hebel für 03041 statt 03042

## Artefakte (Projektordner)
`kv_bellheim.py` · `Honorar_Dashboard_Bellheim_Q2_2026.html` · `Aktionsliste_Bellheim_Q2_2026.html` · `snapshots/*.json` · `KV-PDFs/` · `tomedo-Exporte/`

## Lernpunkte
- CON-Fortsetzungsseiten haben keine Tabellen-Kopfzeile → Spaltenpositionen über Seiten mitführen.
- SKT-Zeilen: Name kann mit Begründungsspalte kollidieren (nur 1 Leerzeichen) → Fallback-Split an „, Die ".
- Treffer-Zählung wie KV: je GOP-Eintrag, nicht je Patient.
