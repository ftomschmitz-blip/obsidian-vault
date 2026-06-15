# Hermes Agent – API Keys & Modell-Setup

Stand: 2026-06-15

## Übersicht

| Dienst | Modell | Verwendung | Status |
|--------|--------|------------|--------|
| Anthropic Claude | Claude Sonnet 4.6 (MAX) | Haupt-Modell | ✅ Aktiv |
| OpenRouter | google/gemini-2.5-flash | Cron Jobs & Automatisierung | ✅ Aktiv |
| Google AI Studio | Gemini 2.5 (Flash/Pro) | Fallback wenn Claude-Token leer | ✅ Aktiv |

---

## Eingerichtete API Keys

### OpenRouter
- **URL:** https://openrouter.ai
- **Verwendung:** Cron Jobs (Morning Briefing, KI-Recherche)
- **Modell:** `google/gemini-2.5-flash`
- **Key hinterlegt in:** `/opt/data/.env` → `OPENROUTER_API_KEY`

### Google Gemini (AI Studio)
- **URL:** https://aistudio.google.com
- **Projekt:** Hermes Agent Api Key
- **Key hinterlegt in:** `/opt/data/.env` → `GEMINI_API_KEY`
- **Key endet auf:** `...CpJQ`
- **Hinweis:** Kostenpflichtig (Kreditkarte hinterlegt) – aber sehr günstig

---

## Cron Jobs & Modell-Zuweisung

| Cron Job | Schedule | Modell | Lieferung |
|----------|----------|--------|-----------|
| Morning Briefing – Tom | Mo–Fr 05:00 Uhr | gemini-2.5-flash (OpenRouter) | Telegram |
| KI in der Arztpraxis | 1. des Monats 08:00 | gemini-2.5-flash (OpenRouter) | Lokal |
| Obsidian Vault Auto-Sync | Alle 30 Min | – (Shell Script) | Lokal/Still |

---

## Modell wechseln

Wenn Claude-Token leer sind → in Telegram schreiben:
> „Wechsel auf Gemini"

Oder manuell: `/model` → OpenRouter → `google/gemini-2.5-pro`

---

## Obsidian Sync Setup

- **Vault:** `/Users/tschmitz/ObsidianVaults/Second Brain Tom`
- **GitHub Repo:** https://github.com/ftomschmitz-blip/obsidian-vault (privat)
- **Server Vault:** `/opt/data/obsidian-vault`
- **Sync:** Obsidian Git Plugin (alle 15 Min Push) + Server Pull (alle 30 Min)

### Ablauf
```
iPhone/Mac → Obsidian Git (15 Min) → GitHub → Hermes Pull (30 Min) → Server
```
