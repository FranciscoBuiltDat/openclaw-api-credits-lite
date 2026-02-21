# API Credits Lite

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Display API credit balances with video game style health bars. Lightweight version for 5 core providers with API auto-tracking and manual sync.

![Health Bar Example](https://via.placeholder.com/600x200?text=Health+Bar+Preview)

## Installation

```bash
# Clone the repository
git clone https://github.com/openclaw/openclaw-api-credits-lite.git
cd openclaw-api-credits-lite

# Optional: install requests for API auto-checks
pip install requests
```

## Quick Start

1. **Configure your providers** in `config.json`:
   ```json
   {
     "providers": {
       "anthropic": {
         "enabled": true,
         "max_credits": 50.00,
         "current_credits": 45.00
       }
     }
   }
   ```

2. **View your credits**:
   ```bash
   python3 scripts/show_credits.py
   ```

3. **Auto-check OpenAI balance**:
   ```bash
   OPENAI_API_KEY=sk-... python3 scripts/check_openai.py --update
   ```

4. **Manual sync for others**:
   ```bash
   python3 scripts/sync_provider.py anthropic 42.50
   ```

## Features

- **Visual Health Bars** - Video game style credit display
- **5 Core Providers** - Anthropic, OpenAI, OpenRouter, Mistral, Groq
- **API Auto-Check** - Automatic balance checks for OpenAI, OpenRouter, Vercel
- **Manual Sync** - Update from provider consoles
- **Threshold Alerts** - Warning when credits are low
- **Minimal Dependencies** - Pure Python + requests (for API checks)

## Supported Providers

### API-Based (Automatic)
| Provider | API Key Env | Script |
|----------|------------|--------|
| OpenAI | `OPENAI_API_KEY` | `check_openai.py` |
| OpenRouter | `OPENROUTER_API_KEY` | `check_openrouter.py` |
| Vercel | `VERCEL_AI_GATEWAY_KEY` | `check_vercel.py` |

### Manual Sync Only
| Provider | Console URL |
|----------|-------------|
| Anthropic | console.anthropic.com |
| Mistral | console.mistral.ai/billing |
| Groq | console.groq.com/settings/billing |

## Usage

### Display Credits

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

OpenAI 🟩
[██████████] 100% ($100.00/$100.00)

━━━━━━━━━━━━━━━━━━━━━
⚠️ Anthropic is low
```

### Auto-Check API Providers

```bash
# Check OpenAI
OPENAI_API_KEY=sk-... python3 scripts/check_openai.py --update

# Check OpenRouter
OPENROUTER_API_KEY=sk-... python3 scripts/check_openrouter.py --update

# Check all APIs at once
python3 scripts/check_all_apis.py --update
```

### Manual Sync

```bash
# From Anthropic console
python3 scripts/sync_provider.py anthropic 45.00

# With max credits
python3 scripts/sync_provider.py openai 85.00 100.00
```

### Add Credits

```bash
python3 scripts/topup.py anthropic 25
```

## Pro Version

Need automatic JSONL tracking and more providers? Check out [api-credits-pro](https://github.com/openclaw/openclaw-api-credits-pro):

- Auto-tracking from OpenClaw session logs (includes prompt caching!)
- 16+ providers (AWS Bedrock, Azure, GCP, xAI, etc.)
- Heartbeat integration
- Cloud provider SDK support
- Usage analytics

## Contributing

Contributions welcome! Please read [SECURITY.md](SECURITY.md) before contributing.

## License

MIT - see [LICENSE](LICENSE)
