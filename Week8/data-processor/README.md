# Week 8: Automating with CSV and JSON Data

**จัดทำโดย:** จันทรณภา จอมทอง 683380574-6 (อ้างอิงจากตัวอย่างของอาจารย์)

This project focuses on programmatic interaction with two fundamental structured plaintext data formats: CSV (Comma Separated Values) and JSON (JavaScript Object Notation), using Python's built-in `csv` and `json` modules.

## Implemented Features

* **CSV Reading (DictReader)**: Reads CSV files using the first row as headers, so each row is a dictionary.
* **CSV Writing (DictWriter)**: Writes lists of dictionaries back to CSV with proper headers.
* **CSV Data Processing**: Calculates total sales and average price, and filters records by a minimum amount.
* **JSON Reading (`json.load`)**: Parses JSON files into Python lists and dictionaries.
* **JSON Writing (`json.dump`)**: Saves Python objects to JSON with pretty-printing.
* **JSON Data Manipulation**: Updates stock levels of existing products and adds a new product.
* **Modular Design**: Logic is split into `csv_handler.py`, `json_handler.py`, and `utils.py`.
* **Robustness**: Basic error handling for file operations and data parsing.

## How to Run

```bash
cd Week8/data-processor
python main.py
```

No extra packages are needed (`csv` and `json` are built-in).

## Output

* `data/output_filtered_sales.csv` — filtered sales records plus a summary row.
* `data/output_updated_inventory.json` — updated product inventory.

## Project Structure

```
data-processor/
├── src/
│   ├── __init__.py
│   ├── csv_handler.py     # CSV read/write/process
│   ├── json_handler.py    # JSON read/write/process
│   └── utils.py           # Logging, file path helpers
├── data/
│   ├── input_sales.csv
│   └── input_inventory.json
├── main.py
├── .gitignore
└── README.md
```
