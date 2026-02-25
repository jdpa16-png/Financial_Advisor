# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Revolut Financial Warden** — automatically categorizes transactions from Revolut CSV exports. The project is in early development; core scripts (`process.py`, `mapping.json`) are planned but not yet implemented.

## Commands

This project uses `uv` for Python dependency management (Python ≥ 3.9).

```bash
# Install dependencies
uv sync

# Run the main entry point
uv run main.py

# Run a specific script (e.g. process.py once implemented)
uv run process.py

# Run inside Docker (keeps container alive for manual exec)
ANTHROPIC_API_KEY=... docker compose up -d
docker compose exec financial-agent uv run process.py
```

## Architecture

- **`main.py`** — placeholder entry point; real logic lives in `process.py` (to be created).
- **`process.py`** (planned) — reads CSVs from `./Fin_Data/` and maps transaction descriptions to categories using `mapping.json`.
- **`mapping.json`** (planned) — keyword → category dictionary; the source of truth for categorization rules. When an unknown merchant is encountered, add it here.
- **`Fin_Data/`** — drop Revolut CSV/XLSX exports here before running `process.py`. This directory is gitignored.
- **`docker-compose.yml`** — runs a `python:3.12-slim` container with the repo mounted at `/app` and `ANTHROPIC_API_KEY` injected from the environment.

## Key Workflow

1. Place new Revolut CSV exports in `Fin_Data/`.
2. Run `uv run process.py`.
3. If a merchant is unrecognized, suggest a category and update `mapping.json`.

## Dependencies

- `pandas` — CSV parsing and data manipulation.
- `openpyxl` — reading/writing `.xlsx` files.

## Important Constraints

- CSV and XLSX files are gitignored — never commit raw financial data.
- `.env` files are also gitignored.