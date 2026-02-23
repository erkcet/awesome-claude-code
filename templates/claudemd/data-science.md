# CLAUDE.md — Data Science / ML Template

<!-- Copy this file to your project root as CLAUDE.md and customize it. -->

## Project Overview

- **Name:** <!-- Your project name -->
- **Description:** <!-- One-liner about what this project does -->
- **Stack:** Python 3.12+, pandas, scikit-learn <!-- add extras: PyTorch, TensorFlow, XGBoost, Hugging Face, etc. -->
- **Package manager:** pip <!-- or conda, mamba, uv, poetry -->
- **Virtual env:** `.venv/` (activate with `source .venv/bin/activate`) <!-- or conda env -->
- **Experiment tracking:** <!-- MLflow, Weights & Biases, DVC, none -->

## Commands

| Action | Command |
|--------|---------|
| Create venv | `python -m venv .venv` |
| Activate venv | `source .venv/bin/activate` |
| Install deps | `pip install -r requirements.txt` |
| Create conda env | `conda env create -f environment.yml` |
| Activate conda env | `conda activate project-name` |
| Start Jupyter | `jupyter lab` |
| Run notebook (CLI) | `jupyter nbconvert --execute notebook.ipynb` |
| Run pipeline | `python src/pipeline.py` |
| Run training | `python src/train.py` |
| Run evaluation | `python src/evaluate.py` |
| Run tests | `pytest tests/` |
| Lint | `ruff check .` |
| Format | `ruff format .` |
| Type check | `mypy src/` |
| DVC pull data | `dvc pull` |
| MLflow UI | `mlflow ui --port 5000` |

## Project Structure

```
data/
├── raw/                       # Original, immutable data
├── interim/                   # Intermediate transformed data
├── processed/                 # Final datasets for modeling
└── external/                  # Third-party data sources
notebooks/
├── 01_eda.ipynb               # Exploratory data analysis
├── 02_feature_engineering.ipynb
├── 03_modeling.ipynb
└── 04_evaluation.ipynb
src/
├── __init__.py
├── pipeline.py                # End-to-end pipeline orchestration
├── train.py                   # Model training entry point
├── evaluate.py                # Model evaluation entry point
├── predict.py                 # Inference / prediction script
├── data/
│   ├── __init__.py
│   ├── load.py                # Data loading and ingestion
│   ├── clean.py               # Data cleaning and validation
│   └── features.py            # Feature engineering
├── models/
│   ├── __init__.py
│   ├── baseline.py            # Baseline model
│   └── transformer.py         # Model definitions
├── utils/
│   ├── __init__.py
│   ├── io.py                  # File I/O helpers
│   ├── plotting.py            # Visualization utilities
│   └── metrics.py             # Custom metrics
└── config.py                  # Hyperparameters and configuration
models/
├── trained/                   # Serialized trained models (.pkl, .pt, .onnx)
└── checkpoints/               # Training checkpoints
reports/
├── figures/                   # Generated plots and charts
└── results/                   # Evaluation metrics, tables, summaries
configs/
├── train_config.yaml          # Training hyperparameters
└── data_config.yaml           # Data pipeline configuration
tests/
├── test_data.py               # Data loading / transformation tests
├── test_features.py           # Feature engineering tests
└── test_model.py              # Model input/output shape tests
```

## Conventions

- Notebooks are for exploration and presentation only. All reusable logic must live in `src/`. Notebooks import from `src/`.
- Notebook naming: prefix with a number for ordering (e.g., `01_eda.ipynb`, `02_feature_engineering.ipynb`). Clear output before committing.
- Data is immutable: never modify files in `data/raw/`. Write transformed data to `data/processed/`.
- Data pipeline: raw -> clean -> feature engineering -> processed. Each step is a separate function or script that can run independently.
- Experiment tracking: log all runs with hyperparameters, metrics, and artifacts. Use MLflow, W&B, or a simple CSV log at minimum.
- Model versioning: save models with metadata (training date, dataset hash, metrics, hyperparameters). Use a consistent naming scheme (e.g., `model_v2_2024-01-15.pkl`).
- Reproducibility: set random seeds, pin dependency versions, document data sources and preprocessing steps.
- Use type hints in all `src/` code. Docstrings on all public functions (describe inputs, outputs, shapes).
- Config over code: put hyperparameters and paths in YAML config files or environment variables, not hardcoded in scripts.
- Large files: do not commit data or model files to git. Use `.gitignore`, DVC, or Git LFS.

## Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `DATA_DIR` | No | Override default data directory path |
| `MODEL_DIR` | No | Override default model output directory |
| `MLFLOW_TRACKING_URI` | No | MLflow tracking server URI |
| `WANDB_API_KEY` | No | Weights & Biases API key |
| `WANDB_PROJECT` | No | Weights & Biases project name |
| `OPENAI_API_KEY` | No | OpenAI API key (for LLM-based features) |
| `HF_TOKEN` | No | Hugging Face access token |
| `AWS_ACCESS_KEY_ID` | No | AWS credentials (S3 data access) |
| `AWS_SECRET_ACCESS_KEY` | No | AWS credentials (S3 data access) |
| `DATABASE_URL` | No | Database connection string (for data ingestion) |
| `CUDA_VISIBLE_DEVICES` | No | GPU device selection (e.g., `0,1`) |
| `RANDOM_SEED` | No | Global random seed for reproducibility (default: `42`) |

## Known Issues / Notes

<!-- Add anything Claude should know: WIP areas, tech debt, gotchas -->
