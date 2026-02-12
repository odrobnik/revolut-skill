# Revolut Skill

Unified web automation for Revolut: login, logout, accounts, transactions, portfolio.

## Setup

Create `{workspace}/revolut/config.json`:

```json
{
  "users": {
    "oliver": {},
    "sylvia": { "pin": "060716" }
  }
}
```

## Usage
```bash
python3 scripts/revolut.py --user oliver login
python3 scripts/revolut.py --user oliver accounts
python3 scripts/revolut.py --user oliver transactions --from 2025-01-01 --until 2026-01-31
python3 scripts/revolut.py --user sylvia portfolio
```

If only one user is configured, `--user` can be omitted.

## Security
- **Auto-logout by default**: Data commands auto-delete session state after completion (no persistent auth on disk). Use `--keep-session` to override.
- Output paths (`--out`) restricted to workspace root or `/tmp`
- No `.env` file loading — credentials in `config.json` only
- Session state stored under `{workspace}/revolut/` only (ephemeral by default)
- User names sanitized against path traversal
- The `pin` field is a non-secret identification number for the Revolut auth flow

## Notes
- Playwright is required (`pip install playwright && playwright install chromium`).
- QR code screenshot saved to `/tmp/openclaw/revolut/revolut_qr.png` during login.
- See `SKILL.md` for agent usage guidance.
