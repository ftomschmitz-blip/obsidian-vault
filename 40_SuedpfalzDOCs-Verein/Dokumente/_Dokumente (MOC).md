---
typ: moc
rolle: SuedpfalzDOCs
---
# 📑 Dokumente – SüdpfalzDOCs / gGmbH

> **Prinzip:** Die PDF/Scan bleibt in deiner Ablage (iCloud-Hüte). Hier liegt nur eine **schlanke Metadaten-Notiz** pro *wichtigem* Dokument (Vertrag, Bescheid, Rechnung mit Frist) — damit du es **wiederfindest** und **Fristen** verfolgst. Nicht jedes PDF braucht eine Notiz.
> Neue Notiz: Vorlage **Dokument**.

## ⏰ Dokumente mit offener Frist
```dataview
TABLE WITHOUT ID file.link AS "Dokument", frist AS "Frist", absender AS "Von"
FROM "40_SuedpfalzDOCs-Verein"
WHERE typ = "dokument" AND frist AND status != "erledigt"
SORT frist ASC
```

## 📋 Alle Dokumente (neueste zuerst)
```dataview
TABLE WITHOUT ID file.link AS "Dokument", datum AS "Datum", kategorie AS "Kategorie", absender AS "Von"
FROM "40_SuedpfalzDOCs-Verein"
WHERE typ = "dokument"
SORT datum DESC
```
