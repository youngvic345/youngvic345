[← Back to profile](../README.md)

# Tax-invoice & cost reconciliation

**SQL · PostgreSQL views · Python · tax-authority (eTIMS) integration**

Two data-quality problems that quietly distorted a business's numbers: sales that did not match what was reported to the tax authority, and average-cost figures that were wrong in the stock and margin reports.

## Tax-invoice (eTIMS) reconciliation

- Pulls sales and credit notes from the fiscal-device provider and matches them against the business's own sales records.
- Built in three phases: ingestion, matching, and a review surface. Exceptions are visible and explainable instead of lost in a spreadsheet.
- Output includes owner-only pages in the analytics platform.

## Cost and inventory reconciliation (seven phases)

- Traced wrong average costs to their cause: negative cost-per-unit entries leaking into every cost fallback.
- Fixed it **at the database-view level**, so the 19 dependent views were corrected at once rather than patching each report.
- Added a POS stock snapshot upload so system stock can be compared with what the till believes.
- New owner reports built on the corrected data, and the CEO pack's closing stock value was repointed to the corrected view.
- Rebuilt a historical stock series for the first half of the year, with no gaps.

## Why it matters

Reports are only as good as the layer under them. Fixing the root cause once made every downstream report right and removed a whole class of "why does this number differ?" questions.
