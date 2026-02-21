# Security Policy

## Overview

This skill tracks API credit balances. While it doesn't store API keys, it handles billing information that should be kept private.

## Security Best Practices

### 🔐 No Credentials in Code

This skill does **NOT** store or require API keys. It only tracks dollar amounts.

If you integrate with API checking scripts, follow these rules:

1. **Use Environment Variables**
   ```bash
   export OPENAI_API_KEY="your-key-here"
   ```

2. **Never Hardcode Keys**
   - No API keys in config files
   - No tokens in scripts
   - No credentials in git

### 📁 Protected Files

The following files contain runtime data and **should not be committed**:

- `config.json` - Your actual credit balances
- `*.log` - Any log files

These are excluded by `.gitignore`.

### ✅ What This Skill Does

- ✅ Stores only dollar amounts locally
- ✅ Reads from/writes to local config file
- ✅ No network requests (display-only)
- ✅ No credentials required

### ❌ What This Skill Does NOT Do

- ❌ Store any API keys
- ❌ Make network requests
- ❌ Transmit data anywhere
- ❌ Access external services

## Data Handling

**Stored locally:**
- Credit balances (dollar amounts)
- Provider names
- Last sync timestamps

**NOT stored:**
- API keys
- Auth tokens
- Account identifiers

## Minimum Permissions

This skill requires only:
- Read/write access to its own directory
- No network access
- No system access

## Reporting Security Issues

If you discover a security vulnerability:

1. **DO NOT** open a public GitHub issue
2. Email: security@openclaw.dev
3. Include:
   - Description of the vulnerability
   - Steps to reproduce
   - Potential impact

We will respond within 48 hours.

## Audit Status

- **Last audit:** 2026-02-21
- **Status:** ✅ No hardcoded credentials
- **Status:** ✅ No sensitive data exposure
- **Status:** ✅ Safe patterns for credential docs

---

**Remember:** This is a display-only tool. Keep your actual API keys secure using environment variables or a credential manager.
