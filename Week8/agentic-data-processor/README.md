# Week 8 (ADV): Agentic Data Processing (Advanced CSV & JSON Workflows)

**จัดทำโดย:** จันทรณภา จอมทอง 683380574-6 (อ้างอิงจากตัวอย่างของอาจารย์)

This project demonstrates an "Agentic Data Processor" that orchestrates complex data manipulation workflows for CSV and JSON files based on a declarative JSON configuration. It showcases advanced data transformation, cross-format conversion, and robust state management within the agent.

## Key Concepts Demonstrated

* **Agentic Workflow Orchestration**: The `DataAgent` reads a pipeline defined in `configs/data_pipeline_config.json` and executes tasks sequentially, managing the flow of data between steps.
* **Internal Data Store**: The agent maintains an in-memory `data_store` (`self.data_store`) to pass intermediate processed data (as Python lists of dicts or nested dicts/lists) between tasks using user-defined keys.
* **Advanced CSV Processing**:
  * Loading CSV data as a list of dictionaries (`DictReader`).
  * **Aggregation**: Grouping data by a field (e.g., `Customer`) and performing calculations (e.g., `sum` of `Amount`).
  * Saving processed data back to CSV (`DictWriter`).
* **Advanced JSON Processing**:
  * Loading and saving JSON data.
  * **Dynamic Updates**: Applying multiple updates to nested JSON structures using a dot-notation path, including `set` and `add_to_list` operations.
  * **Querying Data**: Extracting specific values from nested JSON using a path.
* **Cross-Format Conversion**:
  * Converting a list of dictionaries (from CSV) into a JSON-compatible Python object.
  * (Conceptual) Converting JSON back to CSV, handling simple nested structures.
* **Modularity**: Code is organized into `csv_tasks.py`, `json_tasks.py`, `conversion_tasks.py`, `config_parser.py`, and `utils.py` for clarity and reusability.
* **Robustness**: Includes comprehensive error handling and an audit logging mechanism to track every step of the agent's execution.

## Setup & How to Run

1. **Clone the repository:**
   ```bash
   git clone https://github.com/parima1209/683380574-6_sec1_script_programming.git
   cd 683380574-6_sec1_script_programming/Week8/agentic-data-processor
   ```

2. **Install Dependencies:**
   Python's `csv` and `json` modules are built-in, so no extra packages are needed.
   It's recommended to use a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate.bat
   ```

3. **Prepare Input Data Files** (already included in `data/`):
   * `data/input_sales.csv` — sample sales data; the first row is the header.
   * `data/input_inventory.json` — sample product inventory data.

4. **Review `configs/data_pipeline_config.json`:**
   * This file defines the entire data processing workflow.
   * Make sure the `file_path` values point to the input files, relative to the project root.
   * Feel free to modify the `tasks` to experiment with different aggregations, filters, or JSON transformations.

5. **Run the script:**
   ```bash
   python main.py
   ```
   The script will execute the pipeline defined in `data_pipeline_config.json`:
   * Load `input_sales.csv`.
   * Aggregate sales by customer and save to `data/processed_sales_by_customer.csv`.
   * Convert the raw sales data to JSON and save to `data/sales_data.json`.
   * Load `input_inventory.json`.
   * Apply various updates to the inventory data (stock levels, add new product).
   * Query a specific detail from the updated inventory.
   * Save the updated inventory data to `data/updated_inventory.json`.
   * Generate a detailed `audit_report_*.json` in the `reports/` directory.

## Project Structure

```
agentic-data-processor/
├── src/
│   ├── __init__.py              # Python package marker
│   ├── data_agent.py            # Core agent logic: orchestrates tasks and manages data state
│   ├── csv_tasks.py             # Loading, saving, aggregating, filtering CSVs
│   ├── json_tasks.py            # Loading, saving, updating, querying JSON
│   ├── conversion_tasks.py      # Converting CSV <-> JSON
│   ├── config_parser.py         # Loads and validates the JSON pipeline configuration
│   └── utils.py                 # Logging, directory creation, audit logging utilities
├── configs/
│   └── data_pipeline_config.json  # Declarative JSON configuration for the data pipeline
├── data/
│   ├── input_sales.csv                 # Sample input CSV
│   ├── input_inventory.json            # Sample input JSON
│   ├── processed_sales_by_customer.csv # Output: Aggregated sales CSV
│   ├── sales_data.json                 # Output: Sales data converted to JSON
│   └── updated_inventory.json          # Output: Modified inventory JSON
├── main.py                      # Application entry point
├── .gitignore                   # Files/folders to ignore in Git
└── README.md                    # This project overview
```

## Debugging Advanced Data Workflows

* **`FileNotFoundError`**:
  * Ensure `input_sales.csv` and `input_inventory.json` are in the `data` directory.
  * Check that `file_path` entries in `data_pipeline_config.json` point to your files (relative to the project root).
* **`KeyError` in CSV/JSON Processing**:
  * Verify that CSV column names and JSON keys exactly match what the tasks expect (e.g., `Customer`, `Amount` in CSV; `id`, `stock` in JSON).
  * For JSON `path` updates/queries, ensure the dot-notation path (`key1.key2.index`) reflects your JSON structure.
* **Invalid JSON/CSV Format**:
  * Use a validator or your IDE to check `input_inventory.json` and `data_pipeline_config.json` for syntax errors (missing commas, wrong brackets, etc.).
  * For CSVs, ensure consistent delimiters and proper quoting if fields contain commas.
* **Data Not Changing / Processing Incorrectly**:
  * **Check `input_data_key` and `output_data_key`**: the `output_data_key` of one task must match the `input_data_key` of the next task if you want to chain them.
  * **Review Task Parameters**: double-check `group_by_field`, `aggregate_field`, `operator`, `path`, `value` in the config.
  * **Log Output**: read the console logs and the generated `audit_report_*.json` in `reports/` for task status, errors, and intermediate data.
  * **Type Conversion Issues**: `csv_to_json` performs basic type conversion (int, float, boolean, null). More complex data (e.g., dates) needs extra handling in `conversion_tasks.py`.

## Extension Ideas (Future Work)

* **More Complex CSV Joins/Merges**: SQL-like `INNER JOIN` / `LEFT JOIN` across multiple CSV files; consider `pandas` for large datasets.
* **Advanced JSON Transformations**: Use Jinja2 templates or JMESPath queries inside the config.
* **Data Validation with Schemas**: Use `jsonschema` to validate input data before processing.
* **Error Handling Strategies**: Retries, fallback operations, or notifications on failure.
* **Conditional Task Execution**: Run tasks based on the results of previous tasks.
* **Dynamic Source/Destination**: Build `file_path` dynamically (e.g., `output_path_prefix + date + .csv`).
* **External Data Sources**: Load data from web APIs, databases, or cloud storage.
* **Web Interface**: A simple Flask/Streamlit app to upload configs and view results and audit logs.
