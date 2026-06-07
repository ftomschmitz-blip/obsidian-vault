---
typ: moc
rolle: SuedpfalzDOCs
---
# 🗳️ Sitzungen & Protokolle – SüdpfalzDOCs / gGmbH

> Vorstandssitzungen, Mitgliederversammlung, gGmbH-Termine. Vorlage **Meeting** verwenden, hier ablegen.

## 🗓️ Alle Sitzungen (neueste zuerst)
```dataview
TABLE WITHOUT ID file.link AS "Sitzung", datum AS "Datum", teilnehmer AS "Teilnehmer"
FROM "40_SuedpfalzDOCs-Verein/Sitzungen"
WHERE typ = "meeting"
SORT datum DESC
```

## ✅ Offene Action Items aus Sitzungen
```tasks
not done
path includes 40_SuedpfalzDOCs-Verein/Sitzungen
sort by due
```
