# PII Redaction Tool — Notebook Prototype

**Option B** — Take-home assignment for Value AI Labs  
Notebook-style prototype (Jupyter / Google Colab) that detects and redacts PII from text and PDFs and produces token-redacted text + a JSON audit log.

## Summary
This prototype accepts PDF (scanned or digital) and text input, detects PII (emails, phones, names, locations, orgs, credit-card-like numbers) using a hybrid pipeline (regex + spaCy NER + OCR), and outputs:

- `redacted_output.txt` — token-labeled redacted text, page-separated  
- `redaction_log.json` — structured detection log with confidence heuristics


## Demo Video 
Watch the walkthrough video here:  
🔗 https://go.screenpal.com/watch/cTXZ2InqT88

## How to run (Google Colab)
1. Open `PII_Redaction_Notebook.ipynb` in Colab.  
2. Run cells top-to-bottom.  
3. When prompted, either upload your PDF or use the sample path included in the notebook:  
   `/mnt/data/Redact-Samples (2).pdf`  
   (Alternatively: `/mnt/data/Take-home assignment (1).pdf`)  
4. After running, download `redacted_output.txt` and `redaction_log.json`.



## Approach
- **Extraction**: PyMuPDF for text extraction; Tesseract OCR fallback for scanned pages.  
- **Detection**: Deterministic regex for high-precision items (emails, phones, credit-card-like), spaCy NER for PERSON/GPE/ORG.  
- **Redaction**: Token-label replacement in text (e.g., `[EMAIL_1]`, `[NAMES_1]`).  
- **Logging**: JSON with detected items and confidence heuristics for auditability.

## Limitations & notes
- Accuracy depends on OCR quality for scanned pages.  
- NER-based name detection can produce false positives; confidence scores are provided in the log.  
- For production-grade use, consider adding whitelist/blacklist, improved address parsing (libpostal), and manual review UI.



## Contact
Prepared by Fariha Taneem.
