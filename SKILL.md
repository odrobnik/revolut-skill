---
name: revolut
description: "Revolut web automation via Playwright: login/logout, list accounts, and fetch transactions."
summary: "Revolut banking automation: login, accounts, transactions, portfolio."
version: 1.1.1
homepage: "https://github.com/odrobnik/revolut-skill"
metadata: {"openclaw": {"emoji": "💳", "requires": {"bins": ["python3", "playwright"], "python": ["playwright"]}}}
---

# Revolut Banking Automation

Fetch current account balances, investment portfolio holdings, and transactions for all wallet currencies and depots in JSON format for automatic processing. Uses Playwright to automate Revolut web banking.

**Entry point:** `{baseDir}/scripts/revolut.py`

## Authentication

Requires **2FA via the Revolut app** on your iPhone. When the script initiates login, a QR code and approval link are generated. Either open the link on the device where you have your Revolut app installed, or scan the QR code with the device you use for authorization.

The QR code image is saved to `/tmp/openclaw/revolut/revolut_qr.png` and the path is output as `QR_IMAGE:<path>` for the agent to send.

## Configuration

Create `{workspace}/revolut/config.json`:

```json
{
  "users": {
    "oliver": {},
    "sylvia": { "passcode": "123456" }
  }
}
```

- **Single user**: auto-selected, no `--user` needed.
- **Multiple users**: `--user` is required.
- **passcode**: optional 6-digit app passcode for auto-entry.

## Commands

```bash
python3 {baseDir}/scripts/revolut.py --user oliver login
python3 {baseDir}/scripts/revolut.py --user oliver accounts
python3 {baseDir}/scripts/revolut.py --user oliver transactions --from YYYY-MM-DD --until YYYY-MM-DD
python3 {baseDir}/scripts/revolut.py --user sylvia portfolio
python3 {baseDir}/scripts/revolut.py --user oliver invest-transactions --from YYYY-MM-DD --until YYYY-MM-DD
```

## State Files

Per-user session state stored in `{workspace}/revolut/`:
- `state_{user}.json` + `.pw-state_{user}-profile/`

## Notes
- Output paths (`--out`) are sandboxed to workspace or `/tmp`.
- No `.env` file loading — credentials in config.json only.
