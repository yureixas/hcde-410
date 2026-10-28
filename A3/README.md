# A3 — Watching the Machine

A starter notebook for HCDE 410 Assignment 3, in which **AI is the subject of study, not the author.** You investigate the reliability and reproducibility of large language models (LLMs) through a small mixed-methods study, then reflect on what it means for trustworthy research.

## What this notebook is

`A3_watching_the_machine_starter.ipynb` is a scaffold with prompts and empty cells for you to fill in as you work. It walks through five parts:

1. **Prior practice** — a short written reflection on how you currently use LLMs and what they assume about your reliability.
2. **Reproducibility probe** — pick one task with a *checkable* answer, run the same prompt **3 times in one model** and **once in a second model**, and log every run verbatim in a spreadsheet (prompt, model, version, timestamp, output, verified, notes), exported as `a3_runs.csv` and loaded into a pandas DataFrame. A short helper cell summarizes the log (run count, distinct outputs, verification tally).
3. **Observation** — watch 1–2 people do a comparable task with an LLM (with permission, no audio/video, nothing personal or sensitive), take timestamped field notes, and group them into themes in a second spreadsheet, exported as `a3_codes.csv`.
4. **Synthesis & reflection** — bring the probe and observation together into one account about trustworthy, reproducible research and what the student will change in their own AI use.
5. **Competency declaration & AI use** — state which course competencies the work demonstrates (*qualitative & mixed-methods inquiry*, *reproducible analysis*, *ethical & societal reasoning*) and disclose any AI use per course policy.

## Deliverable & workflow

- Fill in each section directly in the notebook (name and date at the top).
- Commit to your `hcde-410` repo **as you work** — commit history is part of what you hand in.
- Do the analysis and writing yourself: in this assignment AI is your subject, not your author.

## How to run

Open `A3_watching_the_machine_starter.ipynb` and run the cells. The only dependency is:

- `pandas`

The notebook does not fetch external data. It loads two CSV files you create from your own runs and field notes: `a3_runs.csv` and `a3_codes.csv`. Header-only templates of both are included in this folder; open them in Google Sheets or Excel, fill them in, download as CSV, and upload them here with the same names.

## License

Released under the MIT License — see [`LICENSE`](./LICENSE).
