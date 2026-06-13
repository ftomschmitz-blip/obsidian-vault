---
typ: session
datum: 2026-06-13
hut: übergreifend
tags: [token-sparen, ollama, lokal, claude-optimierung]
---
# Lokaler Ollama-Direktzugang (Open WebUI)

## Anlass
Frage: „Wie spare ich Token und arbeite trotzdem effizient?" — dabei Fehlannahme aufgedeckt:
Tom dachte, alles laufe **erst lokal auf Ollama** und greife nur bei Bedarf auf kostenpflichtige Claude-Token zu.

## Korrektur des Denkmodells (wichtig)
- **Es gibt keinen automatischen „erst lokal, dann Claude"-Vorfilter.**
- Jede Unterhaltung mit Claude läuft **komplett über die Cloud** (kostenpflichtig).
- Ollama wird **nur** genutzt, wenn Claude bewusst das `ollama-mcp`-Tool aufruft — und diese Entscheidung kostet selbst Claude-Token.
- Bild: Claude = Generalunternehmer (immer am Werk, schreibt die Rechnung), Ollama = Subunternehmer für Routine-Jobs.
- **Echtes Gratis-Arbeiten** geht nur über einen **lokalen Direktkanal ohne Claude dazwischen**.

## Umgesetzt
- **Open WebUI** installiert: `uv tool install --python 3.11 open-webui` (isoliertes Python 3.11, System-Python 3.14 unangetastet).
- Verbunden mit headless `ollama serve` (:11434), Oberfläche auf **http://localhost:8080**.
- Telemetrie aus (`ANONYMIZED_TELEMETRY=false`, `DO_NOT_TRACK=true`, `SCARF_NO_ANALYTICS=true`), Offline-Betrieb.
- **Kein Autostart** (Akku) — Steuerung über `~/.local/bin/ollama-ui`:
  - `ollama-ui start` · `ollama-ui stop` · `ollama-ui status`
- Hochlauf + Health getestet (`{"status":true}`) ✅.

## Offen (Tom)
1. Im Browser einmalig **lokalen Admin-Account** anlegen (erster Account = Admin, bleibt lokal).
2. Modell wählen: `llama3.2` (Routine) · `gemma4` (Texte) · `qwen3:8b` (Reasoning/Medizin) · `nomic-embed-text` (RAG/Embeddings).

## Faustregel lokal (gratis) vs. Claude (kostenpflichtig)
| Aufgabe | Wohin |
|---|---|
| Klassifizieren, taggen, kurze Fragen | lokal (llama3.2) |
| Texte schreiben/zusammenfassen, übersetzen | lokal (gemma4) |
| Medizinische Texte sorgfältig auswerten, langes Reasoning | lokal (qwen3:8b) |
| PDF/Dokument lokal befragen (RAG) | lokal (qwen3:8b + Upload) |
| Werkzeuge/Aktionen: Mail, Kalender, Obsidian, Dateien | Claude |
| Aktuelle Infos / Websuche / Recherche | Claude |
| Orchestrierung über mehrere Apps/Skills | Claude |
| Code, der real laufen/getestet werden muss | Claude |

**Merksatz:** Reines *Nachdenken über Text* → lokal. *Etwas tun, nachschauen oder über Apps koordinieren* → Claude.

⚠️ Lokale Modelle sind schwächer, ohne Internet/Tools — top für „schnell, gratis, vertraulich", aber für Verlässlichkeit bei Wichtigem bleibt Claude die bessere Wahl.

## Zusätzlicher Spar-Haupthebel
Session-Disziplin: neuer Chat pro Thema (mitgeschleppter Kontext ist der eigentliche Kostentreiber), `/compact` bei langen Threads.
