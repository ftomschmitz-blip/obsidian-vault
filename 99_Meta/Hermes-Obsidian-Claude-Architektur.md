# 🧠 Die ultimative Agenten-Landschaft: Hermes Agent, Obsidian & Claude

Diese Architektur beschreibt die optimale Verknüpfung von **Hermes Agent (VPS)**, **Claude (Lokal)** und **Obsidian (Lokal/VPS)** zu einer intelligenten, hocheffizienten Agenten-Landschaft. Sie verbindet die Echtzeit-Fähigkeiten eines lokalen Rechners mit der autonomen Power eines rund um die Uhr laufenden Servers.

---

## 🗺️ System-Architektur im Überblick

```
┌─────────────────────────────────────────────────────────────────────────┐
│                       LOKALER RECHNER (Mac / PC)                        │
│                                                                         │
│  ┌─────────────────┐    (Local REST API)    ┌────────────────────────┐  │
│  │ Claude Desktop  │◄──────────────────────►│ Obsidian App (Lokal)   │  │
│  │ (Cursor / IDE)  │                        │                        │  │
│  └────────┬────────┘                        └───────────┬────────────┘  │
└───────────┼─────────────────────────────────────────────┼───────────────┘
            │                                             │
            │ (SSH stdio Bridge:                          │ (Auto-Push/Pull:
            │  "hermes mcp serve")                        │  Obsidian Git v2.38)
            ▼                                             ▼
┌───────────┼─────────────────────────────────────────────┼───────────────┐
│           │            REMOTE SERVER (Hostinger VPS)    │               │
│           ▼                                             ▼               │
│  ┌─────────────────┐                        ┌────────────────────────┐  │
│  │  Hermes Agent   │◄──────────────────────►│ Obsidian Vault (VPS)   │  │
│  │  (MCP Server)   │  (Direkter Dateipfad)  │                        │  │
│  └─────────────────┘                        └────────────────────────┘  │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## 🏛️ Die 3 Säulen der Kopplung

### Säule 1: Der Git-Sync (Die "Single Source of Truth")
Damit alle Agenten (der lokale Claude und der remote Hermes) auf demselben Wissensstand arbeiten, dient ein **privates GitHub-Repository** als Brücke.
* **Lokal (Rechner):** Das Community-Plugin **Obsidian Git** (v2.38+) committet und pusht Änderungen automatisch zu GitHub.
  * *Einstellung unter "Automatic" (ganz oben):* 
    * `Auto commit interval (minutes)`: `15`
    * `Auto push interval (minutes)`: `15`
* **Remote (VPS):** Ein agentenloser Hermes-Cronjob (`141e7cc673f9`) führt alle 30 Minuten das Skript `obsidian-sync.sh` aus (`git pull --rebase 2>&1`), um das VPS-Vault auf dem neuesten Stand zu halten. Wenn Hermes selbst Änderungen vornimmt, pusht er diese direkt zurück.

---

### Säule 2: Lokaler Claude-Obsidian-MCP
Damit dein lokaler **Claude Desktop** oder deine IDE (wie **Cursor**) in Echtzeit auf deine lokalen Notizen zugreifen kann, binden wir Obsidian als MCP-Server ein.
1. **In Obsidian:** Installiere das Plugin **Local REST API**.
   * Aktiviere HTTPS.
   * Generiere einen API-Schlüssel (Token).
2. **In Claude Desktop:** Trage den Obsidian-MCP-Server von Markus Pfundstein (`MarkusPfundstein/mcp-obsidian`) in deine `claude_desktop_config.json` ein:
```json
{
  "mcpServers": {
    "obsidian": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "-e",
        "OBSIDIAN_API_KEY=dein_api_key_hier",
        "-e",
        "OBSIDIAN_PORT=27124",
        "mcp/server/obsidian"
      ]
    }
  }
}
```
*(Alternativ kann dies auch ohne Docker direkt über Node.js gestartet werden).*

---

### Säule 3: Remote VPS-Hermes-MCP (SSH-Bridge)
Dies ist der **mächtigste Hebel**: Du kannst deinen lokalen Claude Desktop über eine sichere SSH-Verbindung direkt mit dem Hermes Agent auf dem VPS koppeln. Hermes dient dann als remote MCP-Server!
* Trage Folgendes in deine lokale `claude_desktop_config.json` ein:
```json
{
  "mcpServers": {
    "hermes-vps": {
      "command": "ssh",
      "args": [
        "-t",
        "dein_vps_user@deine_vps_ip",
        "/opt/hermes/.venv/bin/hermes mcp serve"
      ]
    }
  }
}
```
* **Der Effekt:** Dein lokaler Claude kann nun über Hermes auf dem VPS Shell-Befehle ausführen, dort Docker-Container verwalten, Backups fahren, Skripte ausführen oder Web-Recherchen im schnellen Server-Netzwerk machen.

---

## ⚡ Der geniale Workaround: Die "Asynchrone Inbox-Task-Queue"

Wenn du unterwegs bist oder nicht aktiv am Terminal arbeiten willst, kannst du eine rein textbasierte Schnittstelle nutzen.

1. **Erstelle eine Datei:** `Inbox/Agent_Inbox.md`
2. **Schreibe Aufgaben als Checkboxen auf:**
   ```markdown
   # 🤖 Agenten-Inbox
   
   - [ ] Aufgabe: Führe eine tiefgehende Recherche zu "Generative AI in Health IT" durch. Schreibe die Ergebnisse in `Recherchen/Health_IT_GenAI.md`.
   - [ ] Aufgabe: Prüfe die Auslastung unseres VPS-Speicherplatzes und erstelle einen Report in `System/VPS_Status.md`.
   ```
3. **VPS-Hermes liest mit:** Ein Cronjob auf dem VPS läuft alle 15 Minuten und liest diese Datei.
4. **Ausführung:**
   * Hermes erkennt offene `- [ ] Aufgabe:...` Boxen.
   * Er startet im Hintergrund einen Subagenten (`delegate_task`) oder führt die Aufgabe selbst aus.
   * Sobald fertig, schreibt er die Datei am Zielort (z.B. `Recherchen/Health_IT_GenAI.md`) und ändert den Status in der Inbox auf `- [x] Aufgabe... (Erledigt am [Datum])`.
5. **Ergebnis:** Du öffnest dein Obsidian am Mac oder iPhone, und die fertig recherchierten Dokumente sind bereits da – vollkommen magisch, ohne eine einzige Zeile Code eingetippt zu haben.

---

## 💡 Best Practices & Profi-Tipps

### 1. Merge-Konflikte im Keim ersticken
Da sowohl du als auch die Agenten an den Dateien arbeiten, nutze immer `--rebase` beim Git-Pull (im VPS-Sync-Skript bereits integriert).
* **Tipp:** Platziere eine `.gitignore` im Root deines Vaults, um temporäre Obsidian-Dateien vom Git-Sync auszuschließen:
  ```
  .obsidian/workspace.json
  .obsidian/workspace-mobile.json
  .obsidian/plugins/obsidian-git/
  ```

### 2. SSH Key-Authentifizierung ohne Passwort
Damit die SSH-Verbindungen von Claude Desktop zum VPS reibungslos im Hintergrund laufen, richte unbedingt eine passwortlose SSH-Key-Authentifizierung (`ssh-copy-id`) ein.

### 3. Agenten-Leitplanken setzen (Tirith & YOLO-Mode)
* Erlaube Hermes auf dem VPS im Gateway-Modus nicht standardmäßig jeden Befehl unbestätigt auszuführen (`approvals.mode: smart`).
* Für den MCP-Betrieb via SSH mit deinem lokalen Claude kannst du den YOLO-Mode aktivieren, da du hier selbst am Steuer sitzt.

---
*Erstellt am 16. Juni 2026 von deinem Hermes Agent.*
