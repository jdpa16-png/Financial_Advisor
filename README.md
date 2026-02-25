# Revolut Financial Warden

### Goal
Automatically categorize transactions from Revolut CSV exports located in `./workspace/`.

### Tech Stack
- **Language:** Python (managed via `uv`)
- **Logic:** `process.py` reads CSVs and maps descriptions to categories.
- **Brain:** `mapping.json` stores the keyword -> category pairs.

### Instructions for Claude
1. When a new CSV is added to `/workspace`, run `uv run process.py`.
2. If a merchant is unknown, suggest a category and update `mapping.json`.
3. Never upload CSV files to GitHub.