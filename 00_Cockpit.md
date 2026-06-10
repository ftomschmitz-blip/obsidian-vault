---
typ: cockpit
---
# 🧭 Cockpit

Zentrale Übersicht aller offenen Aufgaben aus deinen Rollen.
**So entstehen Aufgaben:** Schreib in *irgendeiner* Notiz eine Zeile `- [ ] Text 📅 2026-06-10`. Sie taucht hier automatisch auf. Fälligkeit per 📅-Symbol (Tasks-Plugin setzt es bequem über das Kommando „Tasks: Create or edit task").

**Projekt-Ebene:** 🧵 [[00_Faeden]] — laufende Handlungsfäden, Top-3 der Woche, Parkplatz.

## 🔴 Überfällig
```tasks
not done
due before today
sort by due
group by folder
```

## 🟠 Heute fällig
```tasks
not done
due on today
sort by priority
group by folder
```

## 🟡 Demnächst (nächste 14 Tage)
```tasks
not done
due after today
due before in two weeks
sort by due
group by folder
```

## 📋 Alle offenen Aufgaben nach Rolle
```tasks
not done
sort by due
group by folder
limit 150
```

## ⚪ Offen, ohne Fälligkeit
```tasks
not done
no due date
group by folder
```

---
## 🗓️ Letzte Tagesnotizen
```dataview
LIST
FROM "999_Tagesnotizen"
SORT file.name DESC
LIMIT 7
```
