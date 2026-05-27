# Are Old Books Longer?

A data science mini-project for Eli, using real library data from the [Open Library API](https://openlibrary.org/developers/api).

**The question:** Do books written 100 years ago have more pages than books written today? Or fewer? Or about the same?

We'll fetch metadata for thousands of fiction books across the last ~150 years, then use pandas + matplotlib to find out.

## Setup

### If you have Anaconda installed (Eli's setup)

Anaconda already ships with pandas, matplotlib, requests, and JupyterLab — you don't need to install anything. Just open the **Anaconda Prompt**, navigate to this folder, and start JupyterLab:

```
cd path\to\eli-example
jupyter lab
```

### Without Anaconda (macOS / Linux)

One-time setup (creates an isolated Python environment so we don't mess up your system Python):

```
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Every time you come back to the project:

```
source .venv/bin/activate
jupyter lab
```

### Without Anaconda (Windows)

If you don't have Python yet, install **Python 3.12** from the Microsoft Store — it's the easiest path on Windows (no PATH wrangling).

One-time setup, in PowerShell:

```
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```

Every time you come back:

```
.venv\Scripts\activate
jupyter lab
```

### Once JupyterLab is running

JupyterLab will open in your browser. Navigate to `notebooks/are-old-books-longer.ipynb` and start running cells with Shift+Enter.

## About the data

The [Open Library Search API](https://openlibrary.org/dev/docs/api/search) is a free, no-auth-required JSON API maintained by the Internet Archive. It catalogues over 30 million books. We use the `number_of_pages_median` field, which is Open Library's best estimate of a book's page count across all editions of that work.

## What's in here

- `notebooks/are-old-books-longer.ipynb` — the main notebook. Walks through fetching the data, cleaning it, and plotting.
- `data/` — cached API responses live here so we don't re-hit the API every time.
- `requirements.txt` — Python packages.
