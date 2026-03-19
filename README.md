# Data Analytics / Data Science Capstones

This repository contains mini and full capstones for Practera data science modules.

## Launch in Browser

Open the interactive JupyterLite environment (no install required):

**[Launch JupyterLite](https://intersective.github.io/data-capstones/lab/index.html)**

Everything runs in your browser via [Pyodide](https://pyodide.org/) — no server, no setup, no accounts.

## Notebooks

### Practera Capstones

| Capstone | Notebook | Direct Link |
|----------|----------|-------------|
| Exploratory Data Analysis | `practera/eda/task.ipynb` | [Open](https://intersective.github.io/data-capstones/lab/index.html?path=practera/eda/task.ipynb) |
| Data Cleaning | `practera/cleaning/task.ipynb` | [Open](https://intersective.github.io/data-capstones/lab/index.html?path=practera/cleaning/task.ipynb) |
| Clustering | `practera/clustering/task.ipynb` | [Open](https://intersective.github.io/data-capstones/lab/index.html?path=practera/clustering/task.ipynb) |
| Regression | `practera/regression/task.ipynb` | [Open](https://intersective.github.io/data-capstones/lab/index.html?path=practera/regression/task.ipynb) |

### SkillsBuild Sustainability

| Capstone | Notebook | Direct Link |
|----------|----------|-------------|
| NYC Water Project 1 | `skillsbuild/sustainability/nyc_water_project_1.ipynb` | [Open](https://intersective.github.io/data-capstones/lab/index.html?path=skillsbuild/sustainability/nyc_water_project_1.ipynb) |
| NYC Water Project 2 | `skillsbuild/sustainability/nyc_water_project_2.ipynb` | [Open](https://intersective.github.io/data-capstones/lab/index.html?path=skillsbuild/sustainability/nyc_water_project_2.ipynb) |

## How It Works

This repo uses [JupyterLite](https://jupyterlite.readthedocs.io/) to serve a full Jupyter environment as a static site on GitHub Pages. On every push to `trunk`, a GitHub Action builds the site and deploys it.

Packages available in the Pyodide kernel include pandas, numpy, matplotlib, scikit-learn, scipy, and statsmodels. Additional pure-Python packages (like plotly) can be installed at runtime via `%pip install`.

## Known Limitations

- **Google Sheets notebook** (`practera/eda/task_gsheets.ipynb`) is excluded — it requires server-side Google API credentials which aren't available in a browser environment.
- **NYC Water notebooks** fetch data from the NYC Open Data API. Pyodide supports HTTP fetch, but `pd.read_json(url)` may need to use `pyodide.http.open_url()` instead. The local fallback file `project_2_data.json` is included.
- **Excel files** referenced by the cleaning and clustering notebooks (`test_data.xlsx`, `processed_data.xlsx`, `mainstream_media.xlsx`) are not in this repo and were previously provided externally.
- **First load** takes 10-20 seconds as Pyodide downloads and initializes in your browser. Subsequent visits are faster due to browser caching.

## Development

To build the JupyterLite site locally:

```bash
pip install -r requirements.txt
mkdir -p content
cp -r practera content/
cp -r skillsbuild content/
jupyter lite build --contents content --output-dir dist
```

Then serve `dist/` with any static file server:

```bash
python -m http.server -d dist 8000
```

## Previous Setup

This repo previously used BinderHub + nbgitpuller via `intersective/binder-base`. That approach has been replaced with JupyterLite for a lighter-weight, zero-infrastructure solution.
