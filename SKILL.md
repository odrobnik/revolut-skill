---
name: revolut
description: "Revolut web automation via Playwright: login/logout, list accounts, and fetch transactions."
summary: "Revolut banking automation: login, accounts, transactions."
version: 0.2.0
metadata: {"openclaw": {"emoji": "💳", "requires": {"bins": ["python3", "playwright"]}}}
---

# Revolut (Web Automation)

Unified UX for Revolut: **login**, **logout**, **accounts**, **transactions**.

**Entry point:** `{baseDir}/scripts/revolut.py`

## Commands

```bash
python3 {baseDir}/scripts/revolut.py login
python3 {baseDir}/scripts/revolut.py logout
python3 {baseDir}/scripts/revolut.py accounts
python3 {baseDir}/scripts/revolut.py transactions --account EUR

# Revolut Invest (stocks)
python3 {baseDir}/scripts/revolut.py portfolio
python3 {baseDir}/scripts/revolut.py invest-transactions --from YYYY-MM-DD --until YYYY-MM-DD
```

## Notes
- Uses Playwright (QR code login).
- Session state stored in `~/clawd/revolut_state.json` by default (override with `--state`).
