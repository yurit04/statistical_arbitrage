# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A research monorepo for statistical arbitrage and algo-trading strategies. Each research project lives under `projects/` and shares a common internal Python package (`trading_research`) that lives in `src/`.

## Environment setup

Uses **uv** (not pip directly). From repo root:

```bash
uv venv --prompt stat-arb
source .venv/bin/activate
uv pip install -e ".[dev]"
```

Register the Jupyter kernel once after setup:
```bash
python -m ipykernel install --user --name "stat-arb" --display-name "stat arb"
```

## Commands

```bash
# Run tests
pytest

# Lint
ruff check src/ tests/

# Type check
mypy src/
```

No Makefile exists; run commands directly.

## Architecture

### Shared package: `src/trading_research/`

Editable-installed as `trading_research`. Submodules follow a data-pipeline layering:

| Module | Intended role |
|---|---|
| `data/` | Data fetching/loading (yfinance, parquet via pyarrow) |
| `features/` | Feature engineering (technical indicators, factors) |
| `modeling/` | Model training/eval (sklearn, xgboost, lightgbm, torch) |
| `portfolio/` | Portfolio construction and weighting (prado methods, etc.) |
| `execution/` | Backtesting / execution simulation |
| `utils/` | Shared helpers |
| `viz/` | Plotting utilities (matplotlib, seaborn) |

All submodules are currently scaffolded (empty `__init__.py`). Add code here when logic should be shared across projects.

### Projects: `projects/<project-name>/`

Each project is self-contained and follows this layout:

```
projects/<name>/
  README.md
  notebooks/        # Jupyter notebooks (primary workspace)
  scripts/          # Standalone Python scripts
  configs/          # YAML configs
  outputs/          # gitignored — data, model artifacts, plots
```

Current projects:
- **attention_factors_stat_arb** — attention-mechanism-based factors for stat arb (has a reference paper PDF)
- **ml_pairs_trading** — ML-driven pairs trading strategies
- **masters_meets_prado_portfolio** — portfolio construction using Prado methods
- **ml_technical_analysis_sp500** — ML on technical indicators for S&P 500
- **momentum_transformer** — transformer-based momentum strategy (has a reference paper PDF)

### Key conventions
- Notebooks import from `trading_research` using editable install — no `sys.path` hacks needed.
- `projects/**/outputs/` and `data/` are gitignored; never commit model artifacts or downloaded data.
- Reference papers (PDFs) live alongside the project they inform.
