# ETL Extract and Transform Lab

**Name:** Iranzi Innocent  
**Student ID:** 67xxxx 

## Description

This project is a take-home lab for **DSA 2040A - Lab 3 (US 2025)**, extended to include both the **Extraction** and **Transformation** phases of the ETL (Extract, Transform, Load) process.

It demonstrates:
- Full Extraction
- Incremental Extraction
- Three distinct data transformations

All using a synthetic sales dataset.

The implementation is in a Jupyter Notebook (`etl_extract.ipynb`) and includes functionality to:

- **Generate a Dataset**: Create a realistic dataset (`custom_data.csv`) with 105 records.
- **Full Extraction**: Load the entire dataset.
- **Incremental Extraction**: Extract only new records using `last_extraction.txt`.
- **Transformations**: Clean, enrich, and restructure data.
- **Test Incremental Extraction**: Append records and verify accurate incremental processing.
- **Documentation**: Step-by-step explanations using Markdown cells.

All project files are organized in the folder `ETL_Extract_IranziInnocent_670513` and hosted on a public GitHub repository.

## Tools Used

- **Python**: Core programming language.
- **pandas**: For data manipulation and transformation.
- **Jupyter Notebook**: For interactive development and documentation.
- **Git/GitHub**: For version control and project sharing.
- **random, datetime**: For synthetic data generation.


## Project Structure


ETL\_Extract\_IranziInnocent\_670513/
├── etl\_extract.ipynb           # Main Jupyter Notebook
├── custom\_data.csv             # Synthetic sales dataset
├── last\_extraction.txt         # Tracks last extraction timestamp
├── transformed\_full.csv        # Transformed full dataset
├── transformed\_incremental.csv # Transformed incremental dataset
├── .gitignore                  # Git ignore file
└── README.md                   # Project documentation


## How to Reproduce

### 1. Install Python

Download Python 3.11+ from [python.org](https://www.python.org/)  
During installation, check the option **“Add Python to PATH”**.

### 2. Install Required Libraries

Install dependencies using pip:

pip install jupyter pandas


### 3. Clone the Repository

Ensure Git is installed from [git-scm.com](https://git-scm.com/).
Clone the repository:


> Replace `yourusername` with your actual GitHub username.

### 4. Navigate to the Project Directory


cd ETL_Extract_IranziInnocent_67xxxx


### 5. Launch Jupyter Notebook

jupyter notebook

This will open a browser window showing the project files.

### 6. Run the Notebook

* Open `etl_extract.ipynb`
* Click **Kernel > Restart & Run All**

The notebook will:

* Generate `custom_data.csv` if it doesn't exist
* Perform full and incremental extraction
* Apply data transformations
* Save transformed data
* Append new records and reprocess incrementally


## Data Source

The dataset (`custom_data.csv`) is synthetic, created using Python libraries. Each record includes:

* `transaction_id`: Unique ID (1–105)
* `date`: Dates from Jan 1, 2025 to Apr 5, 2025
* `customer_id`: Random integer between 1000–9999
* `product`: One of `Laptop`, `Phone`, `Tablet`, or `Headphones`
* `amount`: Random value between \$50 and \$1000 (2 decimal places)

### Transformed Datasets Add:

* `product_category`: Grouped as `Computing`, `Mobile`, or `Accessories`
* `month`: Extracted month from `date` (e.g., `2025-01`)

## Implementation Details

### 1. Dataset Generation

* Uses `random` and `datetime` to create initial 100 records.
* Appends 5 new records (April 2025).
* Saves to `custom_data.csv`.

### 2. Full Extraction

* Reads and displays entire dataset with `pandas.read_csv()`.

### 3. Incremental Extraction

* Reads last date from `last_extraction.txt`
* Defaults to `2020-01-01` if file is missing.
* Extracts records **on or after** the timestamp.
* Updates `last_extraction.txt`.

### 4. Transformations

Applied to both full and incremental data:

* **Cleaning**: Remove duplicates and impute missing values.
* **Enrichment**: Add `product_category`.
* **Structural**: Convert `date` to datetime and extract `month`.

### 5. Testing Incremental Extraction

* Appends 5 new April 2025 records.
* Re-runs extraction and transformation.
* Verifies only new records are processed.

### 6. Documentation

* Clear markdown sections for each step.
* Well-commented, readable code.


## Notes

* Works on any system with Python, pandas, and Jupyter.
* Handles missing `last_extraction.txt` and missing values.
* Uses `>=` comparison for timestamp-based extraction.
* Repository is public per grading requirements.

