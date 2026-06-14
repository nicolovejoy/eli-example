# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Context

This repo is a teaching project for **Eli** (Nico's kid), who is newly interested in data science and library science. The audience is a learner who is comfortable with Python but new to pandas, matplotlib, and working with public APIs. Bias toward:

- Explaining *why* a data-cleaning or analysis decision was made, not just *what* the code does.
- Small, runnable cells that build on each other.
- Leaving prompts/TODOs for Eli to fill in (hypotheses, observations, stretch goals) rather than handing him a finished report.

If Eli (or Nico on his behalf) asks for a new notebook on a different question, follow the same shape as `notebooks/are-old-books-longer.ipynb`: question → hypothesis prompt → fetch → clean → analyze → plot → reflection prompts → stretch challenges.

## Running things

Setup (one-time):

```
python3 -m venv .venv && source .venv/bin/activate && pip install -r requirements.txt
```

Start JupyterLab:

```
source .venv/bin/activate && jupyter lab
```

## Data source

[Open Library Search API](https://openlibrary.org/dev/docs/api/search) — free, no auth, JSON. Endpoint: `https://openlibrary.org/search.json`. Useful query features:

- Solr-style range queries: `first_publish_year:[1900 TO 1910]`
- Subject filter: `subject:science_fiction`
- Language filter: `language:eng`
- Restrict response with `fields=title,author_name,first_publish_year,number_of_pages_median,language` to keep payloads small.
- `limit=` caps results (max 1000). For broader pulls, paginate with `offset` or split by year ranges.

Be polite — sleep ~200ms between requests. Responses are cached in `data/` so subsequent notebook runs don't re-hit the API; if you change the query, delete the matching `data/*.json` file.

## Notebook conventions

- One question per notebook. Filename = the question, kebab-case.
- Notebooks live in `notebooks/`; cached API data lives in `data/` (gitignored except `.gitkeep`).
- Relative path to data from a notebook: `Path("../data")`.
- Drop NaNs *and* obvious outliers before analysis — explain the outlier threshold in a markdown cell.
- Always include a `decade` derivation (`year // 10 * 10`) when grouping across long time spans; raw years are too noisy.

## What not to do

- Don't refactor the notebook into a Python package or split helpers across multiple files — keep everything visible in the notebook so Eli can read top-to-bottom.
- Don't add type checking, linting configs, or test infrastructure. This is a learning notebook, not a production app.
- Don't suggest deploying this to Vercel or wrapping it in a web app. It's a local JupyterLab project.

<!-- SHARED-CONVENTIONS:BEGIN v=d5e16e653242 — auto-managed, do not edit here; source: prompt-lab/workflow/claude-md-shared.md (edit + re-sync) -->
## Shared conventions

<!-- These are Nico's cross-repo output rules. They're materialized into each repo's
CLAUDE.md so every agent (local, cloud, third-party) sees them as plain text. Source
of truth: prompt-lab/workflow/claude-md-shared.md — edit there and re-sync, never here. -->

- **Clickable URLs.** When pointing at any web destination (dashboard, repo, PR, deploy, settings, docs, localhost), print the full bare URL — `https://example.com` or `http://localhost:8080` — on its own, never just the page's name and never a markdown `[label](url)` link. Nico's terminal auto-linkifies raw `https://` text, so a bare URL is one-click and stays copyable.

- **Number your questions.** Any time you ask Nico more than one question, present them as a numbered list (1., 2., 3.) so he can answer by number with no ambiguity. A single standalone question needs no number.

- **Self-contained smoke-test instructions.** When you ask Nico to manually test or verify an app or website, assume zero carried-over context — he should never scroll back or recall a URL/path/credential from earlier. Always include: the exact URL (full `https://…` or `http://localhost:…`, restated even if mentioned above), the precise steps in order, and what a pass vs. fail looks like. Repetition here is a feature, not clutter.

- **No marker before a copy-paste command block.** Nico's terminal renders markdown bullets (`-`, `*`, `•`) as `●`, which breaks paste into zsh. The line directly above a fenced command block must be a plain-text label ending in a colon — never a bullet, dash, asterisk, or number. For loud copy targets, lead the label with `📋` + bold `COPY THE BELOW`, then a colon, then the block.
<!-- SHARED-CONVENTIONS:END -->
