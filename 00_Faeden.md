---
typ: faeden
aktualisiert: 2026-06-10
---
# 🧵 Handlungsfäden

Projekt-Ebene über dem [[00_Cockpit]]: Was läuft, was ist der nächste Schritt, was hat Priorität.

**Spielregeln:**
1. **Jede Claude-Session** (Code, Desktop, Cowork) aktualisiert am Ende ihren Faden-Block: Stand + Nächster Schritt.
2. **WIP-Limit: max. 7 aktive Fäden.** Neues landet im Parkplatz — aktiviert wird nur im Wochenreview.
3. **Wochenreview (15 Min, freitags oder sonntags):** Tom sagt in irgendeiner Claude-Session „Wochenreview bitte" → Claude liest diese Notiz, geht alle Fäden durch (Was ist passiert? Stockt etwas? Was fliegt raus?), gemeinsam werden die **Top-3 der Woche** neu gesetzt.

Status: 🔴 kritisch/dringend · 🟢 läuft · 🟡 stockt/wartet · ⏸️ geparkt

---

## ⭐ Top-3 dieser Woche *(vorläufig — im ersten Wochenreview bestätigen)*

1. **gGmbH:** Kontostand feststellen → Reichweite → Krisengespräch vorbereiten
2. **Praxis:** Q2/2026-Vorprüfung abarbeiten (Frist 30.06.!)
3. **Organisation:** Kalender-Woche (6-Hüte-Plan Woche 2) wiederholen

---

## Aktive Fäden

### 🔴 gGmbH Liquiditätskrise
- **Hut:** 50_gGmbH · **Stand:** 10.06. (abends) — Leitfaden v2 + rollierender Plan geprüft: Juni nur mit Stundung der Anwaltsrechnung gedeckt (sonst −659 €), Lücke bis 31.12. real 46–81 T€ (nicht 35–40). Krisengespräch im Sparring trainiert; Maßnahmenkatalog mit 10 Beschlusspunkten, Verantwortlichen und Fristen steht: [[Massnahmenkatalog-Liquiditaet-gGmbH-2026-06-10]]
- **Nächster Schritt:** StB-Anfrage §§ 17/18/15a/15b InsO binnen 48 h raus (Anlagen: BWA 04/2026 + Liquiditätsstatus) → Krisengespräch Vorstand terminieren
- **Danach:** Leitfaden-Einstieg auf korrigierte Juni-Lage anpassen · 13-Wochen-Plan-Sachkosten vom GF · Kreis-Termin (Betrauungsmittel)
- **Quellen:** [[2026-06-10-Krisengespraech-Training]] · [[2026-06-10-gGmbH-Liquiditaetskrise-Leitfaden]] · `~/Desktop/Claude /gGmbH Südpfalz/`

### 🔴 Praxis: KV-Abrechnung Q2/2026
- **Hut:** 10_Praxis-Bellheim · **Stand:** 10.06. — Faden ins Cowork-Projekt „Praxis Assistent zur Datenanalyse KV Abrechnungen" übernommen; Detail-Dokument `KV-Abrechnung-Q2-2026_Status.md` im Projektordner angelegt (Kennzahlen, offene Punkte, PDF-Links)
- **Nächster Schritt:** 3 KV-PDFs vom 06.06. in den Projektordner kopieren → dann 29 Hinweisarten analysieren (€-Wirkung, Priorisierung). Parallel: 2 SKT-Scheine hochladen (Abdule, Bülbül), zurückgestellte Fälle (Lytvynov, Leydecker, HZV: Schwind) + Doppelansätze prüfen — **Frist 30.06.**
- **Quellen:** [[00_Wiedervorlage]] (Einträge 04.06. + 06.06.) · Projektordner `~/Documents/Claude/Projects/Praxis Assistent zur Datenanalyse  KV Abrechnungen/`

### 🟡 Organisation: 6-Hüte-Setup (Master-Plan v2)
- **Hut:** übergreifend · **Stand:** 23.05. — Plan v2 steht, Woche 2 (Kalender) muss wiederholt werden
- **Nächster Schritt:** Kalender-Woche neu ansetzen

### 🟡 Blitztext: Hotkeys zum Laufen bringen
- **Hut:** übergreifend · **Stand:** 10.06. — App läuft, Diktat per Menüleisten-Klick funktioniert (inkl. Auto-Paste). Hotkeys gehen nicht — Ursache gefunden: Belegung war falsch notiert, laut Code ist Transkription **`fn + Shift`** (nicht `fn` allein). `AppleFnUsageType` stand wieder auf 3, erneut auf 0 gesetzt.
- **Nächster Schritt:** `fn + Shift` halten → sprechen → loslassen testen. Falls tot: Bedienungshilfen-Berechtigung prüfen (Systemeinstellungen → Datenschutz & Sicherheit → Bedienungshilfen, alte Blitztext-Einträge entfernen, App neu starten)
- **Quellen:** [[2026-06-10-Blitztext-Hotkeys]] · `~/blitztext-app/BlitztextMac/Services/HotkeyService.swift`

### 🟡 Mail-System: Smart-Mailbox-Fixes
- **Hut:** übergreifend · **Stand:** 07.06. — Analyse fertig, 12 statt 6 Mailboxen, 2 FlaggedStatus-Fehler
- **Nächster Schritt:** FlaggedStatus korrigieren (rot=1, orange=2), Duplikate klären, Entscheidung 6 vs. 12
- **Quellen:** [[2026-06-07-Smart-Mailbox-Sortierung]] · [[Mail-System]]

---


### 🟢 Hermes Agent im VCP
- **Hut:** übergreifend · **Stand:** 10.06. (abends) — Setup komplett: Hermes auf Hostinger VPS, Telegram-Gateway aktiv, `/sethome` gesetzt. Erster Cron-Job läuft: Morning Briefing Mo–Fr 7:00 per Telegram (News DE, Wetter Bellheim, Medizin-Update). Zugangsdaten in 1Password
- **Nächster Schritt:** Morgen (11.06.) prüfen, ob das erste Briefing um 7:00 ankommt und Qualität passt → danach weitere Use Cases. Oxylabs-Credits im Blick behalten (Websuche)
- **Regel:** keine Patientendaten/Zugangsdaten/gGmbH-Interna über den Bot (kein E2E)
- **Quellen:** [[2026-06-10-Hermes-Telegram-Setup]]

## ⏸️ Parkplatz

- **Downloads-Rest:** Cloud-Stubs prüfen + MS365-Ablage (aus Bereinigung 30.05.)
- **Festplatte:** nur noch 17 GB frei (97 %) — nächste Kandidaten: icloudmailagent (812 MB), Google-Cache (787 MB)
- **Obsidian-MCP:** recent_changes defekt — bei Gelegenheit fixen oder ersetzen

---

## Erledigt (Kurzarchiv, letzte 5)

- ✅ 10.06. **Blitztext Grundinstallation:** App läuft, Diktat per Menüleisten-Klick + Auto-Paste funktioniert (Hotkeys → eigener Faden)
