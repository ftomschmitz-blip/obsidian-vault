# 🗺️ Schritt-für-Schritt-Anleitung: Hermes, Obsidian & Claude Desktop einrichten

Hallo Tom! 👋 

Diese bebilderte und leicht verständliche Anleitung führt dich Schritt für Schritt durch die Einrichtung deines intelligenten Agenten-Ökosystems. Keine Sorge: Auch wenn du Git-Anfänger bist, ist jeder Schritt so beschrieben, dass nichts schiefgehen kann.

> [!TIP]
> **Visuelle Unterstützung:** Ich habe dir ein wunderschönes, interaktives Architektur-Diagramm direkt in deinem Vault erstellt!
> Du findest es unter: **`99_Meta/Hermes-Obsidian-Claude-Setup-Architektur.html`**
> Mache einfach einen Doppelklick auf diese HTML-Datei auf deinem Mac, um sie im Webbrowser zu öffnen. Sie zeigt dir genau, wie alle Zahnräder ineinandergreifen!

---

## 🗺️ Inhaltsverzeichnis
1. **Phase 1: Git-Synchronisation** (Die Datenbrücke)
2. **Phase 2: Lokaler Claude-Obsidian-Zugriff** (Deine lokale AI)
3. **Phase 3: Remote VPS-Hermes-Kopplung** (Der mächtige Server-Agent)
4. **Fehlerbehebung & Best Practices**

---

## 🛠️ Phase 1: Git-Synchronisation (Die Datenbrücke)
Damit dein lokaler Mac, GitHub und dein VPS-Server immer auf demselben Stand sind, nutzen wir Git im Hintergrund.

### Schritt 1.1: Obsidian Git Plugin auf dem Mac installieren
1. Öffne **Obsidian** auf deinem Mac.
2. Gehe unten links auf das **Zahnrad-Symbol (Einstellungen)**.
3. Klicke links auf **Community-Plugins** und klicke auf **Aktivieren** (falls noch nicht geschehen).
4. Klicke bei "Community-Plugins durchsuchen" auf **Durchsuchen**.
5. Suche nach **"Obsidian Git"** (von Denis Omercic).
6. Klicke auf **Installieren** und danach auf **Aktivieren**.

### Schritt 1.2: Automatisches Speichern einrichten
Das Plugin soll deine Notizen automatisch im Hintergrund hochladen (push) und herunterladen (pull).
1. Klicke in den Obsidian-Einstellungen links unter "Community-Plugins" auf **Obsidian Git**.
2. Suche den Bereich **Automatic** ganz oben:
   * **`Vault backup interval (minutes)`**: Trage hier `15` ein. (Das bedeutet: Alle 15 Minuten committet und speichert Obsidian deine Änderungen).
   * **`Auto pull interval (minutes)`**: Trage hier `15` ein. (Holt Änderungen von GitHub ab).
   * **`Auto push after backup`**: Aktiviere diesen Schalter. (Lädt deine Änderungen sofort nach dem Backup zu GitHub hoch).
3. Schließe die Einstellungen. Obsidian speichert ab jetzt vollautomatisch alle 15 Minuten!

---

## 🔌 Phase 2: Lokaler Claude-Obsidian-Zugriff (Deine lokale AI)
Damit deine lokale Claude Desktop App direkt auf deine Notizen zugreifen kann, richten wir eine sichere lokale Schnittstelle (API) ein.

### Schritt 2.1: Local REST API Plugin in Obsidian einrichten
1. Gehe in Obsidian wieder in die **Einstellungen** ➔ **Community-Plugins** ➔ **Durchsuchen**.
2. Suche nach **"Local REST API"** (von Markus Pfundstein).
3. Klicke auf **Installieren** und **Aktivieren**.
4. Klicke links in den Einstellungen auf **Local REST API**:
   * **`Enable HTTPS`**: Lass diesen Schalter **aktiviert** (grün).
   * Klicke auf **`Generate API Key / Token`**.
   * Kopiere diesen Schlüssel (eine lange Zeichenkette) in die Zwischenablage und speichere ihn kurz in einer leeren Notiz. Wir brauchen ihn gleich!
   * Der Standard-Port ist `27124`.

### Schritt 2.2: Claude Desktop konfigurieren
Nun sagen wir Claude auf deinem Mac, wie er auf Obsidian zugreifen kann.
1. Öffne den Finder auf deinem Mac.
2. Drücke die Tastenkombination `Shift + Cmd + G` (Gehe zum Ordner) und gib folgenden Pfad ein:
   ```text
   ~/Library/Application Support/Claude/
   ```
3. Suche dort die Datei namens **`claude_desktop_config.json`**.
   * *Hinweis: Falls die Datei oder der Ordner nicht existiert, erstelle sie einfach mit einem Texteditor (z.B. TextEdit).*
4. Öffne die Datei mit einem Texteditor und füge unter `mcpServers` folgenden Block hinzu (ersetze `DEIN_API_KEY_HIER` mit dem Schlüssel aus Schritt 2.1):

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
        "OBSIDIAN_API_KEY=DEIN_API_KEY_HIER",
        "-e",
        "OBSIDIAN_PORT=27124",
        "mcp/server/obsidian"
      ]
    }
  }
}
```

> [!NOTE]
> **Voraussetzung:** Für diese dockerbasierte Variante muss die App **Docker Desktop** auf deinem Mac installiert sein und im Hintergrund laufen. (Einfach kostenlos von docker.com herunterladen und starten).

---

## 🚀 Phase 3: Remote VPS-Hermes-Kopplung (Der Server-Agent)
Dies ist das absolute Highlight: Du kannst deinen lokalen Claude Desktop direkt mit dem remote Hermes Agent auf deinem Hostinger-VPS verbinden. Dadurch kann Claude Befehle auf deinem Server ausführen!

### Schritt 3.1: Passwortlosen SSH-Zugriff einrichten (Sehr wichtig!)
Damit Claude sich ohne lästige Passwortabfragen mit dem VPS verbinden kann, nutzen wir einen SSH-Schlüssel.

1. Öffne das **Terminal** auf deinem Mac (über die Spotlight-Suche `Cmd + Leertaste` -> "Terminal" eingeben).
2. Erstelle einen neuen SSH-Schlüssel, indem du folgenden Befehl eingibst und immer mit `Enter` bestätigst (kein Passwort vergeben!):
   ```bash
   ssh-keygen -t ed25519 -C "tom-macbook"
   ```
3. Kopiere den Schlüssel nun auf deinen VPS. Ersetze `vps_user` mit deinem Benutzernamen (meistens `root`) und `vps_ip` mit der IP-Adresse deines Hostinger VPS:
   ```bash
   ssh-copy-id vps_user@vps_ip
   ```
4. **Testen:** Gib im Terminal `ssh vps_user@vps_ip` ein. Wenn du direkt auf dem Server eingeloggt wirst, ohne nach deinem Passwort gefragt zu werden, hat es perfekt geklappt! Tippe `exit` ein, um die Verbindung wieder zu trennen.

### Schritt 3.2: Remote-MCP zu Claude Desktop hinzufügen
Jetzt verbinden wir die beiden Systeme in der Konfigurationsdatei.
1. Öffne wieder deine **`claude_desktop_config.json`** auf deinem Mac (Pfad: `~/Library/Application Support/Claude/claude_desktop_config.json`).
2. Erweitere den Eintrag unter `mcpServers` um den Server `hermes-vps` (ersetze `vps_user` und `vps_ip` mit deinen echten Serverdaten):

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
        "OBSIDIAN_API_KEY=DEIN_API_KEY_HIER",
        "-e",
        "OBSIDIAN_PORT=27124",
        "mcp/server/obsidian"
      ]
    },
    "hermes-vps": {
      "command": "ssh",
      "args": [
        "-t",
        "vps_user@vps_ip",
        "/opt/hermes/.venv/bin/hermes mcp serve"
      ]
    }
  }
}
```

3. Speichere die Datei ab und starte die **Claude Desktop** App neu.

---

## 🎉 Der Test: Funktioniert alles?
Wenn du Claude Desktop jetzt öffnest, solltest du im Chat-Fenster unten rechts ein kleines **Stecker-Symbol (🔌)** sehen. 
1. Klicke darauf. Dort sollten deine beiden Server gelistet sein: `obsidian` und `hermes-vps`.
2. **Lokaler Test:** Schreibe an Claude: *"Lies meine heutige Tagesnotiz aus Obsidian."* ➔ Claude greift lokal über die API auf dein Obsidian zu!
3. **Remote Test:** Schreibe an Claude: *"Frage Hermes auf meinem VPS nach dem aktuellen Speicherplatz."* ➔ Claude baut im Hintergrund den SSH-Tunnel auf, fragt Hermes auf dem VPS, und dieser liefert die Live-Serverdaten direkt in dein Chat-Fenster!

---

## 💡 Best Practices für Git-Anfänger

### 🤝 Keine Angst vor Konflikten
Da du und Hermes gleichzeitig im selben Vault arbeiten, kann es theoretisch zu "Merge-Konflikten" kommen (wenn ihr dieselbe Zeile am selben Tag bearbeitet). 
* **Die Lösung:** Ich habe das VPS-Sync-Skript so konfiguriert, dass es immer `git pull --rebase` nutzt. Dadurch werden deine lokalen Änderungen auf dem Mac immer priorisiert und sanft über die Änderungen von Hermes drübergelegt.
* **Tipp:** Arbeite am besten in deinen eigenen Ordnern und lass Hermes in der `Inbox/` oder in `99_Meta/` arbeiten. So lauft ihr euch nie in die Quere!

### 🛑 Obsidian-Müll ignorieren
Manchmal speichert Obsidian temporäre Layouts. Erstelle eine Textdatei mit dem Namen **`.gitignore`** direkt im Hauptverzeichnis deines Obsidian-Ordners auf dem Mac und füge diese Zeilen ein, um Unordnung zu vermeiden:
```text
.obsidian/workspace.json
.obsidian/workspace-mobile.json
.obsidian/plugins/obsidian-git/
```

Viel Spaß mit deiner neuen, absolut genialen Agenten-Zentrale! Wenn du Fragen zu einem Schritt hast oder etwas hakt, sag mir einfach Bescheid! 🚀
