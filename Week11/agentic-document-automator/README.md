# Week 11 (ADV): Agentic Document Automator

**จัดทำโดย:** จันทรณภา จอมทอง 683380574-6 (อ้างอิงจากตัวอย่างของอาจารย์)

This project builds an "Agentic Document Automator" that runs a sequence of PDF and Word document tasks defined in a JSON configuration file (`configs/document_automation_config.json`). The `DocumentAgent` reads the plan, executes each task in order, and records every step in an audit report.

## Key Concepts Demonstrated

* **Configuration-Driven Agent**: All tasks, input files and output paths are defined in JSON, so the workflow can be changed without editing code.
* **Word Report Generation (`python-docx`)**: Fills a Word template (`templates/report_template.docx`) with placeholders such as `{{REPORT_TITLE}}` and adds a data table.
* **PDF Watermarking (`reportlab` + `PyPDF2`)**: Creates a rotated, semi-transparent "CONFIDENTIAL" watermark and stamps it on every page.
* **PDF Merging (`PyPDF2`)**: Combines several PDFs into one file.
* **Text Extraction**: Extracts text from both Word and PDF files and saves it to `.txt` files.
* **Audit Logging**: Each task's success or failure is logged and saved as a JSON audit report in `documents/reports/`.

## Tasks in the Pipeline

| # | Task type | Input | Output |
|---|---|---|---|
| 1 | `generate_word_report` | `templates/report_template.docx` | `documents/generated_report.docx` |
| 2 | `apply_pdf_watermark` | `documents/source_document.pdf` | `documents/watermarked_document.pdf` |
| 3 | `merge_pdfs` | `documents/dummy_doc1.pdf`, `documents/dummy_doc2.pdf` | `documents/merged_docs.pdf` |
| 4 | `extract_word_text` | `documents/generated_report.docx` | `documents/extracted_word_text.txt` |
| 5 | `extract_pdf_text` | `documents/source_document.pdf` | `documents/extracted_pdf_text.txt` |

## Setup & How to Run

```bash
pip install -r requirements.txt
python main.py
```

When the run finishes, the console shows `Document automation process completed.` and all output files appear in `documents/`.

## Project Structure

```
agentic-document-automator/
├── src/
│   ├── __init__.py
│   ├── document_agent.py   # Main agent: reads config and dispatches tasks
│   ├── word_tasks.py       # Word report generation and text extraction
│   ├── pdf_tasks.py        # PDF watermark, merge and text extraction
│   ├── config_parser.py    # Loads and validates the JSON configuration
│   └── utils.py            # Logging, directory helpers, audit logging
├── configs/
│   └── document_automation_config.json
├── templates/
│   └── report_template.docx
├── documents/              # Input PDFs and generated outputs
├── main.py
├── requirements.txt
├── .gitignore
└── README.md
```
