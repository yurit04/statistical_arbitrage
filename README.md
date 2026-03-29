# statistical_arbitrage

A research repository containing back-tests and experiments for various stat arb and algo trading strategies.

## Directory structure

```text
statistical_arbitrage/
  pyproject.toml
  README.md
  LICENSE
  .gitignore

  src/
    trading_research/              # shared internal python package
      __init__.py
      data/
        __init__.py
      features/
        __init__.py
      modeling/
        __init__.py
      portfolio/
        __init__.py
      execution/
        __init__.py
      utils/
        __init__.py
      viz/
        __init__.py

  projects/                        # one folder per research project
    attention_factors_stat_arb/
      README.md
      notebooks/
      scripts/
      configs/
      outputs/                     # gitignored
    ml_pairs_trading/
      README.md
      notebooks/
      scripts/
      configs/
      outputs/                     # gitignored
    masters_meets_prado_portfolio/
      README.md
      notebooks/
      scripts/
      configs/
      outputs/                     # gitignored

  docs/
    papers/

  tests/                           # tests for shared package
```

## Getting started (uv + editable install)

This repo is set up as a **single internal Python package** (`trading_research`) using a `src/` layout, so all notebooks can share the same code.

### 1) Create a virtualenv and install dependencies

From repo root:

```bash
uv venv
source .venv/bin/activate
uv pip install -e ".[dev]"
```

### 2) Add a Jupyter kernel (display name: "stat arb")

```bash
python -m ipykernel install --user --name "stat-arb" --display-name "stat arb"
```

Then open Jupyter and select the kernel **"stat arb"**.

### 3) Use shared imports in notebooks/scripts

```python
from trading_research.data import ...
```
