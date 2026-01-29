# Revolut Skill

Import Revolut statements (CSV/PDF) and emit **canonical transactions JSON** compatible with the unified banking schema used by the George and ELBA skills.

## Usage
```bash
# Accounts from PDF
python3 scripts/revolut.py --debug accounts --source pdf --file /path/account-statement.pdf

# Accounts from CSV
python3 scripts/revolut.py --debug accounts --source csv --file /path/revolut_statement.csv

# Transactions (CSV)
python3 scripts/revolut.py transactions \
  --source csv \
  --file /path/revolut_statement.csv \
  --account "Current:EUR" \
  --from 2024-01-01 --until 2024-12-31 \
  --format json \
  --out /tmp/moltbot/revolut/revolut_current_eur_2024 \
  --debug

# Transactions (PDF)
python3 scripts/revolut.py transactions \
  --source pdf \
  --file /path/account-statement.pdf \
  --account "Current:EUR" \
  --from 2024-06-11 --until 2026-01-28 \
  --format json \
  --out /tmp/moltbot/revolut/revolut_from_pdf \
  --debug
```

## Notes
- PDF import uses SwiftText OCR to convert to markdown tables.
- With `--debug`, extra raw fields (fee, running balance) are preserved in output.
- See `SKILL.md` for agent usage guidance.
