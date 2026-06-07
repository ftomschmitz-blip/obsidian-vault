---
typ: moc
rolle: SuedpfalzDOCs
---
# 🗂️ Projekte – SüdpfalzDOCs / gGmbH

> Jede Notiz in diesem Ordner mit Vorlage **Projekt** wird hier automatisch gelistet.
> Neues Projekt: Rechtsklick auf den Ordner → *Neue Notiz aus Vorlage → Projekt* (oder Templater-Befehl).

## 🟢 Aktive Projekte
```dataview
TABLE WITHOUT ID file.link AS "Projekt", deadline AS "Deadline", prioritaet AS "Prio"
FROM "40_SuedpfalzDOCs-Verein"
WHERE typ = "projekt" AND status = "aktiv"
SORT deadline ASC
```

## ✅ Abgeschlossen / pausiert
```dataview
TABLE WITHOUT ID file.link AS "Projekt", status AS "Status"
FROM "40_SuedpfalzDOCs-Verein"
WHERE typ = "projekt" AND status != "aktiv"
SORT file.mtime DESC
```
