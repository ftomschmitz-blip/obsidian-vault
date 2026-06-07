---
typ: dashboard
rolle: SuedpfalzDOCs
---
# 🟠 Dashboard – SüdpfalzDOCs & gGmbH

> Zentrale Steuerung für diesen Bereich. Drei Fragen: **Was ist zu tun? Was läuft? Wo finde ich was?**

## 🚀 Schnellzugriff
- 🗂️ [[_Projekte (MOC)]] · 📑 [[_Dokumente (MOC)]] · 🗳️ [[_Sitzungen (MOC)]]
- 🧭 [[00_Cockpit]] (alle Rollen) · 📄 [[README]]

---
## 1️⃣ Was ist zu tun? — Aufgaben dieses Bereichs

### 🔴 Überfällig
```tasks
not done
due before today
path includes 40_SuedpfalzDOCs-Verein
sort by due
```

### 🟠 Heute & nächste 14 Tage
```tasks
not done
due after yesterday
due before in two weeks
path includes 40_SuedpfalzDOCs-Verein
sort by due
```

### ⚪ Offen ohne Fälligkeit
```tasks
not done
no due date
path includes 40_SuedpfalzDOCs-Verein
```

---
## 2️⃣ Was läuft? — Aktive Projekte
```dataview
TABLE WITHOUT ID file.link AS "Projekt", deadline AS "Deadline", prioritaet AS "Prio"
FROM "40_SuedpfalzDOCs-Verein"
WHERE typ = "projekt" AND status = "aktiv"
SORT deadline ASC
```

---
## 3️⃣ Wo finde ich was? — Dokumente mit Frist
```dataview
TABLE WITHOUT ID file.link AS "Dokument", frist AS "Frist", absender AS "Von"
FROM "40_SuedpfalzDOCs-Verein"
WHERE typ = "dokument" AND frist AND status != "erledigt"
SORT frist ASC
```

---
## 🗳️ Letzte Sitzungen
```dataview
TABLE WITHOUT ID file.link AS "Sitzung", datum AS "Datum"
FROM "40_SuedpfalzDOCs-Verein/Sitzungen"
WHERE typ = "meeting"
SORT datum DESC
LIMIT 5
```


---
📘 Anleitung: [[Effektiv-Nutzung]] · 🛠️ [[System-Anleitung]]