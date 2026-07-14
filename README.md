# Excel Stratified Sampler

A single-page web app that takes a spreadsheet and pulls a **random sample** from it, stratified by one or more category columns. Everything runs locally in your browser — no data is uploaded anywhere.

**▶ Live app: https://zoeyyes.github.io/excel-sampler/**

## Use it

Just open the [live app](https://zoeyyes.github.io/excel-sampler/) — no install needed. Or run it locally by opening `index.html` in any modern browser (double-click it, or serve the folder). SheetJS is bundled in the repo (`xlsx.full.min.js`), so the tool works fully offline.

## How it works

1. **Upload** an `.xlsx`, `.xls`, or `.csv` file (drag-and-drop or click). Pick a sheet if the workbook has several.
2. **Choose category column(s)** from the dropdown. Selecting more than one combines them into value *combos* — e.g. picking `Region` + `Priority` creates strata like `North ⋀ High`, `North ⋀ Low`, `South ⋀ High`, …
3. **Choose how much to extract** via the **Extract by** dropdown:
   - **Percentage of each category** — e.g. 20% of every stratum. Edit any row to override that category's %.
   - **Fixed count per category** — e.g. 5 rows from every stratum. If a category has fewer rows than requested, it takes all of them and a ⚠ warning shows how many categories fell short.
   - **Fixed total across all categories** — you give one target total (e.g. 100) and it's allocated proportionally to category size (largest-remainder method), capped by each category's rows. The total is drawn exactly, or capped to the number of available rows if you ask for more.

   Options: **Rounding** (nearest / floor / ceil, percentage mode), **At least 1 per category** (per-category modes), and a **Reproducible seed** so the same draw repeats exactly.
4. **Draw random sample**, review the preview, then **Download .xlsx** with the sampled rows (original columns preserved).

## Sample size math

- **Percentage:** `sample = round(rowCount × ratio%)`, clamped to the category's row count, with optional "at least 1".
- **Fixed count:** `sample = min(count, rowCount)` per category.
- **Fixed total:** each category gets `floor(target × rowCount / totalRows)`, then leftover rows are handed out by largest fractional remainder (skipping categories already at capacity), so the grand total matches the target exactly (or the row count, if the target is larger).

The **Will sample** stat at the top is the live total across all categories.

## Try it

Load `sample-data.csv` (40 support cases). Pick `Region` + `Priority`, set 50%, and draw — you'll get a proportional random slice of each region/priority combo.
