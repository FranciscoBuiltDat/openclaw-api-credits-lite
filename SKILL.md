---
name: api-credits-lite
description: Display API credit balances for 5 core providers (Anthropic, OpenAI, OpenRouter, Mistral, Groq) with video game style health bars. Manual sync only - perfect for personal usage tracking.
---

# API Credits Lite

Display API credit balances with retro video game health bars. Lightweight version with manual sync for 5 core providers.

## Features

- 🎮 **Video game style health bars** - Visual credit tracking
- 📊 **5 Core Providers** - Anthropic, OpenAI, OpenRouter, Mistral, Groq
- 🔄 **API-based auto-tracking** - Automated checks for OpenAI, OpenRouter, Vercel
- 📋 **Manual sync** - Update balances from provider consoles
- ⚠️ **Threshold alerts** - Warning and critical levels
- 💰 **Top-up tracking** - Record when you add credits

## Quick Start

```bash
# Show current credits
python3 scripts/show_credits.py

# Auto-check OpenAI balance (requires OPENAI_API_KEY env var)
OPENAI_API_KEY=sk-... python3 scripts/check_openai.py

# Auto-check OpenRouter (requires OPENROUTER_API_KEY env var)
OPENROUTER_API_KEY=sk-... python3 scripts/check_openrouter.py

# Manual sync for providers without APIs
python3 scripts/sync_provider.py anthropic 45.00

# Add credits (top-up)
python3 scripts/topup.py openai 25
```

## Supported Providers

| Provider | Console URL | Sync Command |
|----------|-------------|--------------|
| **Anthropic** | console.anthropic.com | `sync_provider.py anthropic <balance>` |
| **OpenAI** | platform.openai.com/usage | `sync_provider.py openai <balance>` |
| **OpenRouter** | openrouter.ai/activity | `sync_provider.py openrouter <balance>` |
| **Mistral** | console.mistral.ai/billing | `sync_provider.py mistral <balance>` |
| **Groq** | console.groq.com/settings/billing | `sync_provider.py groq <balance>` |

## Configuration

Edit `config.json`:

```json
{
  "providers": {
    "anthropic": {
      "enabled": true,
      "max_credits": 50.00,
      "current_credits": 27.50,
      "last_sync": "2026-02-11T03:00:00Z"
    }
  },
  "thresholds": {
    "warning": 50,
    "critical": 25
  }
}
```

## API-Based Auto-Tracking

For providers with APIs, you can auto-check without manual sync:

| Provider | API Key Env | Script |
|----------|------------|--------|
| **OpenAI** | `OPENAI_API_KEY` | `check_openai.py` |
| **OpenRouter** | `OPENROUTER_API_KEY` | `check_openrouter.py` |
| **Vercel** | `VERCEL_AI_GATEWAY_KEY` | `check_vercel.py` |

Usage:

```bash
# Single check
OPENAI_API_KEY=sk-... python3 scripts/check_openai.py

# Update config and show
OPENROUTER_API_KEY=sk-... python3 scripts/check_openrouter.py --update

# Run all enabled API checks
python3 scripts/check_all_apis.py
```

For Anthropic, Mistral, Groq (no public APIs), use manual sync.

## Commands

### Show Credits

```bash
python3 scripts/show_credits.py
```

Output:
```
💰 API Credit Health
━━━━━━━━━━━━━━━━━━━━━

Anthropic 🟧
[████░░░░░░] 42% ($22.97/$54.94)
↳ Last sync: 2m ago

Openrouter 🟩
[████████░░] 85% ($85.50/$100.00)
━━━━━━━━━━━━━━━━━━━━━
⚠️ Anthropic is low
```

### Manual Sync

```bash
# Update balance from console
python3 scripts/sync_provider.py <provider> <balance> [max_credits]

# Examples
python3 scripts/sync_provider.py anthropic 22.97
python3 scripts/sync_provider.py openai 95.00 100.00
```

### Top Up Credits

```bash
python3 scripts/topup.py <provider> <amount>
```

## Health Bar Colors

- 🟩 Green: >75% remaining
- 🟨 Yellow: 50-75%
- 🟧 Orange: 25-50%
- 🟥 Red: <25%

## Scripts

| Script | Description |
|--------|-------------|
| `show_credits.py` | Display health bars |
| `sync_provider.py` | Manual balance sync |
| `topup.py` | Add credits |
| `render_healthbar.py` | Health bar rendering |

## Upgrading to Pro

Need more features? [api-credits-pro](https://github.com/openclaw/openclaw-api-credits-pro) includes:

- 🔄 **Auto-tracking from JSONL** - Automatic cost tracking from session logs
- 🌐 **16+ providers** - All major AI providers
- ☁️ **Cloud provider SDKs** - AWS Bedrock, Azure, GCP Vertex
- 💓 **Heartbeat integration** - Periodic balance checks
- 📈 **Daily/weekly spend tracking** - Usage analytics

## Files

- `config.json` - Provider balances and settings
- `config.example.json` - Example configuration
- `scripts/` - All scripts
