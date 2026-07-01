# Excel Stratified Sampler

A single-page web app that takes a spreadsheet and pulls a **random sample** from it, stratified by one or more category columns. Everything runs locally in your browser — no data is uploaded anywhere.

## Use it

Open `index.html` in any modern browser (double-click it, or serve the folder). An internet connection is needed the first time so it can load the SheetJS library from a CDN.

## How it works

1. **Upload** an `.xlsx`, `.xls`, or `.csv` file (drag-and-drop or click). Pick a sheet if the workbook has several.
2. **Choose category column(s)** from the dropdown. Selecting more than one combines them into value *combos* — e.g. picking `Region` + `Priority` creates strata like `North ⋀ High`, `North ⋀ Low`, `South ⋀ High`, …
3. **Set the extraction ratio.** The default % applies to every category; edit any row in the table to override that category's ratio. Options:
   - **Rounding** — nearest / floor / ceil for the per-category sample size.
   - **At least 1 per category** — never drop a category to zero when its ratio > 0.
   - **Reproducible seed** — enter a seed so the same draw repeats exactly.
4. **Draw random sample**, review the preview, then **Download .xlsx** with the sampled rows (original columns preserved).

## Sample size math

For each category: `sample = round(rowCount × ratio%)`, clamped to the category's row count, with optional "at least 1". The **Will sample** stat at the top is the live total across all categories.

## Try it

Load `sample-data.csv` (40 support cases). Pick `Region` + `Priority`, set 50%, and draw — you'll get a proportional random slice of each region/priority combo.
