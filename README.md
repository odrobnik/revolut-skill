# Revolut Skill

Unified web automation for Revolut: login, logout, accounts, transactions.

## Usage
```bash
python3 scripts/revolut.py login
python3 scripts/revolut.py logout
python3 scripts/revolut.py accounts
python3 scripts/revolut.py transactions --account EUR
```

## Notes
- Playwright is required.
- Session state is stored in `~/clawd/revolut_state.json` by default (override with `--state`).
- See `SKILL.md` for agent usage guidance.
