# PII Redaction Tool — Notebook Prototype

**Option B** — Take-home assignment for Value AI Labs  
Notebook-style prototype (Jupyter / Google Colab) that detects and redacts PII from text and PDFs and produces redacted artifacts.

## Features
- Accepts `.pdf` (digital or scanned) and `.txt`
- Hybrid PII detection: **regex** (emails, phones, credit-card-like) + **spaCy NER** (PERSON, GPE, ORG)
- Text redaction mode (token labels like `[EMAIL_1]`)
- **PDF redaction** with **solid black boxes** overlayed over detected PII (Option A)
- Redaction log: `redaction_log.json`
- Exports: `redacted_output.pdf`, `redacted_output.txt`, `redaction_log.json`
- Notebook is runnable in **Google Colab** (one-click)

## How to run (Colab)
1. Open `PII_Redaction_Notebook.ipynb` in Colab.
2. Run all cells top to bottom.
3. Upload your input PDF or use the provided sample paths:
   - `/mnt/data/Redact-Samples (2).pdf`
   - `/mnt/data/Take-home assignment (1).pdf`
4. After running, download `redacted_output.pdf`, `redacted_output.txt`, and `redaction_log.json`.

## Architecture & Approach
- **Extraction**: PyMuPDF for digital PDF; pytesseract OCR fallback for scanned pages.
- **Detection**: Deterministic regex for structured items + spaCy NER for unstructured entities.
- **Redaction**:
  - Text: token replacement.
  - PDF: compute bounding boxes using PyMuPDF `page.search_for()` for digital PDFs; use pytesseract OCR bboxes for scanned pages, then draw black rectangles with PyMuPDF.
- **Logging**: JSON file enumerating detected PII per page and spans.

## Limitations
- OCR quality depends on scan clarity.
- Address detection is heuristic and may miss or over-detect.
- NER can generate false positives; toggles/whitelists recommended for production.
- LLM-assisted disambiguation is optional but not included by default.

## Next improvements (if more time)
- Add whitelist/blacklist toggles in the notebook
- Integrate an LLM micro-check to disambiguate ambiguous tokens (logged)
- Add a web UI (Streamlit) and authentication for multi-user usage
- Improve address parsing (libpostal)

## Files
- Notebook: `PII_Redaction_Notebook.ipynb`
- Test files (provided): `/mnt/data/Redact-Samples (2).pdf`, `/mnt/data/Take-home assignment (1).pdf`

## Contact
Fariha Taneem 
farihataneem6@gmail.com
