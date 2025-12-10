# Financial Markets Regime Detection & Liquidity Stress Modelling System

**Project:** Market-Regime-Liquidity-Model

**Purpose:** Professional-grade toolkit (RBI FMD / ISI/IIT-level) for detecting market regimes and liquidity stress using volatility, yield-curve and LAF (Liquidity Adjustment Facility) data. The repository contains scripts to download, clean, analyze, model (HMM) and produce policy-ready diagnostics and visualizations.

---

## Repository structure (final layout)

```
Market-Regime-Liquidity-Model/
│
├── data/
│   ├── raw/                      # raw downloaded CSV/XLSX files (do NOT commit large raw files unless necessary)
│   │   ├── NIFTY50_raw.csv
│   │   ├── IndiaVIX_raw.csv
│   │   ├── gsec_1y.csv
│   │   ├── gsec_3y.csv
│   │   ├── gsec_5y.csv
│   │   ├── gsec_10y.csv
│   │   └── laf_liquidity.csv (or .xlsx)
│   └── clean/                    # cleaned outputs from scripts
│       ├── NIFTY50_clean.csv
│       ├── IndiaVIX_clean.csv
│       ├── gsec_tenor_clean.csv
│       ├── laf_liquidity_clean.csv
│       ├── market_dataset.csv
│       ├── market_dataset_with_regimes.csv
│       ├── hmm_model_stats.csv
│       └── yield_metrics.csv
├── src/                          # executable scripts (stepwise)
│   ├── data_download.py          # download NIFTY & IndiaVIX
│   ├── gsec_merge.py             # merge Investing.com tenors
│   ├── laf_load.py               # load/clean RBI LAF file
│   ├── data_prep.py              # join & compute features
│   ├── yield_analysis.py         # yield-curve analysis & plots
│   ├── hmm_regime_detection.py   # HMM modeling + ensemble
│   ├── hmm_diagnostics.py        # diagnostics & summary (optional)
│   └── ...                       # helper scripts
├── plots/                        # generated PNG diagnostics
│   ├── ts_prices_vol_vix.png
│   ├── vol_liquidity_timeseries.png
│   ├── yield_curve_metrics.png
│   ├── yield_curve_snapshots.png
│   └── hmm_regime_ensemble.png
├── requirements.txt              # Python dependencies
├── README.md                     # this file (full instructions)
├── policy_report.pdf             # downloadable executive report (generate locally)
└── LICENSE
```

---

## Quickstart (beginner-friendly)

### 1) Create & activate virtual environment

```powershell
# from project root
python -m venv venv
# Windows PowerShell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\venv\Scripts\Activate.ps1
# or Command Prompt
.\venv\Scripts\activate
```

### 2) Install dependencies

Create `requirements.txt` (see below) and run:

```powershell
pip install -r requirements.txt
```

**Recommended `requirements.txt`** (copy this into a file):

```
numpy>=1.24
pandas>=2.1
matplotlib>=3.7
scikit-learn>=1.2
hmmlearn>=0.2.8
yfinance>=0.2.25
openpyxl>=3.1
xlrd>=2.0
python-dateutil
```

> Note: `hmmlearn` is used for Gaussian HMMs; if you have installation issues on Windows, ensure a compatible numpy/scipy build is installed first.

### 3) Data placement (manual downloads)

Place your downloaded raw files in `data/raw/` using the exact filenames:

* `NIFTY50_raw.csv` (if you used automatic downloader, this is created)
* `IndiaVIX_raw.csv`
* `gsec_1y.csv`, `gsec_3y.csv`, `gsec_5y.csv`, `gsec_10y.csv` (Investing.com exports)
* `laf_liquidity.csv` (or `laf_liquidity.xlsx`) — RBI DBIE Liquidity Operations export

### 4) Run the pipeline step-by-step (recommended order)

```powershell
python src/data_download.py        # downloads NIFTY, IndiaVIX (checks columns)
python src/gsec_merge.py           # merges the four tenor CSVs
python src/laf_load.py             # reads your LAF CSV/XLSX and creates liquidity z-score
python src/data_prep.py            # creates market_dataset.csv and plots
python src/yield_analysis.py       # yield curve visuals and metrics
python src/hmm_regime_detection.py # fits HMMs and builds ensemble
python src/hmm_diagnostics.py      # optional: produces Excel diagnostics
```

**Important:** run each script and confirm output files in `data/clean/` before moving to the next step.

---

## 📘 Author

**Naman Narendra Choudhary**

* B.Tech (ECE)
* Aspiring quant, macro researcher, and future IIM/Harvard/Stanford MBA
* Research-driven mindset blending **engineering + finance + macro policy**
