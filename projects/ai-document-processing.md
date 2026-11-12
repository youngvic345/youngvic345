[← Back to profile](../README.md)

# AI document processing

**React · TypeScript · Gemini API · OCR · fuzzy matching · Netlify · Postgres**

Businesses spend hours keying receipts and supplier invoices into their ERP. These tools turn photos and PDFs into import-ready data, and a second tool cleans messy product names.

## Record processor

- Upload a receipt, invoice or pasted text, choose sales or purchase, set a location code, and pick an output format.
- OCR preview, then a model extracts line items.
- Items are matched to the business's master item list, with a similarity matcher (Jaccard) tuned for pharmaceutical names, then written out as CSV.
- Grew through four generations: a first AI Studio prototype, a Lovable-built version, a multi-provider version (several AI vendors through one interface), and a version with accounts and a database for saved work.
- Documented connection fixes, deployment steps and a validation report comparing matcher accuracy.

## PharmaClean

- Takes inconsistent pharmacy item names and standardises them: spelling, strength, pack size.
- Fast and thinking modes, batching with a configurable size, and retry logic around API rate limits.
- Optional web-search grounding with source links per product, and strict JSON handling so one bad batch does not lose a run.

## What I learned

Matching and validation do more for accuracy than prompt tweaks. Retries, batch sizes and defensive parsing are what make an AI tool usable on a real catalogue.
