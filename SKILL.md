---
name: revolut
description: Import Revolut statements (CSV/PDF) and emit canonical transactions JSON compatible with George/ELBA unified banking schema.
version: 0.1.0
metadata: {"moltbot": {"emoji": "💳", "requires": {"bins": ["python3"]}}}
---

# Revolut Statement Importer

This skill imports Revolut statements (CSV or PDF via SwiftText OCR) and emits **canonical accounts + transactions JSON** compatible with the unified banking schema used by the `george` and `raiffeisen-elba` skills.

## Accounts

### Accounts (PDF)

```bash
python3 {baseDir}/scripts/revolut.py --debug accounts \
  --source pdf \
  --file /path/account-statement.pdf
```

### Accounts (CSV)

```bash
python3 {baseDir}/scripts/revolut.py --debug accounts \
  --source csv \
  --file /path/revolut_statement.csv
```

## Transactions (CSV)

```bash
python3 {baseDir}/scripts/revolut.py transactions \
  --source csv \
  --file /path/revolut_statement.csv \
  --account "Current:EUR" \
  --from 2024-01-01 --until 2024-12-31 \
  --format json \
  --out /tmp/moltbot/revolut/revolut_current_eur_2024 \
  --debug
```

## Transactions (PDF)

Uses SwiftText OCR to convert PDF to Markdown tables first.

```bash
python3 {baseDir}/scripts/revolut.py transactions \
  --source pdf \
  --file /path/account-statement.pdf \
  --account "Current:EUR" \
  --from 2024-06-11 --until 2026-01-28 \
  --format json \
  --out /tmp/moltbot/revolut/revolut_from_pdf \
  --debug
```

## Web Automation (Experimental)

Automate the login flow via Playwright. This requires the user to confirm the login on their mobile device (QR code).

### Login
Run this to establish a session (saved to `revolut_state.json`):
```bash
python3 {baseDir}/scripts/revolut.py login
```
Follow the instructions (scan QR code provided).

### Accounts
Fetch current account balances from the web:
```bash
python3 {baseDir}/scripts/revolut.py accounts
```
Use `--visible` if headless mode is blocked.

### Transactions
Fetch latest transactions:
```bash
python3 {baseDir}/scripts/revolut.py transactions --account EUR
```

### Logout
Clear the session:
```bash
python3 {baseDir}/scripts/revolut.py logout
```

## Notes

Revolut provides extra fields that are useful but not part of the canonical schema (fee, running balance). When `--debug` is enabled, the exporter stores these in the `raw` section.
