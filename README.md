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

All project files are organized in the folder `ETL_Extract_Iranzi_513` and hosted on a public GitHub repository.

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





# DSA-2040A  - Lab 5: Load

## Lab 5 – Load

This section documents the implementation of **Lab 5: Load in ETL** for the DSA 2040A course at USIU-Africa. This lab extends the previous extraction and transformation work by loading the transformed datasets (`transformed_full.csv` and `transformed_incremental.csv`) into a structured format using Pandas DataFrames saved as Parquet files.

### Objective

The primary goal of Lab 5 is to:
- Load both `transformed_full.csv` and `transformed_incremental.csv` into a structured destination.
- Automate the process using a Jupyter Notebook.
- Update the GitHub repository with the new loading implementation.

### Loading Method

- **Approach**: Utilizes Pandas to read the transformed CSV files and save them as Parquet files, an optimized columnar storage format suitable for data analysis.
- **Tools**: 
  - **Python** with **pandas** for data handling.
  - **Jupyter Notebook** (`etl_load.ipynb`) for automation and documentation.
- **Output Format**: Parquet files stored in the `loaded_data/` directory.

### Project Structure Update

The repository structure has been updated to include the following for Lab 5:

ETL_Extract_IranziInnocent_670513/
├── etl_load.ipynb              # New Jupyter Notebook for the loading process
├── loaded_data/                # Directory for loaded Parquet files
│   ├── full_data.parquet       # Parquet file for full transformed data
│   └── incremental_data.parquet # Parquet file for incremental transformed data
├── .gitignore                  # Updated to exclude Parquet files and loaded_data/
└── README.md                   # Updated documentation

### Implementation Details

#### 1. Setup
- **Libraries**: Imported `pandas` and `os` to handle data manipulation and file operations.
- **Directory Creation**: The `loaded_data/` directory was created programmatically using `os.makedirs(data_dir, exist_ok=True)` to store the Parquet output files.
- **File Paths**: Defined as `loaded_data/full_data.parquet` and `loaded_data/incremental_data.parquet` for the full and incremental datasets, respectively.

#### 2. Loading Full Transformed Data
- **Process**: 
  - Read `transformed_full.csv` into a Pandas DataFrame using `pd.read_csv()`.
  - Saved the DataFrame as `full_data.parquet` using `df_full.to_parquet()` with `index=False` to exclude the index column.
- **Outcome**: Successfully loaded all 105 records from `transformed_full.csv`, which includes columns `transaction_id`, `date`, `customer_id`, `product`, `amount`, `product_category`, and `month`.

#### 3. Loading Incremental Transformed Data
- **Process**: 
  - Read `transformed_incremental.csv` into a Pandas DataFrame using `pd.read_csv()`.
  - Saved the DataFrame as `incremental_data.parquet` using `df_inc.to_parquet()` with `index=False`.
- **Outcome**: The `transformed_incremental.csv` file is currently empty due to the `last_extraction.txt` date (2025-04-05) matching the latest data in `custom_data.csv`. As a result, `incremental_data.parquet` is also empty. New records with dates after 2025-04-05 would populate this file upon re-running `etl_extract.ipynb` and `etl_load.ipynb`.

#### 4. Verification
- **Process**: 
  - Read the saved Parquet files back into DataFrames using `pd.read_parquet()`.
  - Displayed the first 5 rows of each file using `.head()` to confirm data integrity.
- **Outcome**: Verification confirmed that `full_data.parquet` matches `transformed_full.csv`, while `incremental_data.parquet` is empty, consistent with the current incremental extraction state.

### Sample Code


# Section 1: Load Setup
import pandas as pd
import os

data_dir = "loaded_data"
os.makedirs(data_dir, exist_ok=True)
parquet_full_path = os.path.join(data_dir, "full_data.parquet")
parquet_inc_path = os.path.join(data_dir, "incremental_data.parquet")

# Section 2: Load Full Transformed Data
df_full = pd.read_csv("transformed_full.csv")
df_full.to_parquet(parquet_full_path, index=False)
print(f"Full transformed data saved to {parquet_full_path}")

# Section 3: Load Incremental Transformed Data
df_inc = pd.read_csv("transformed_incremental.csv")
df_inc.to_parquet(parquet_inc_path, index=False)
print(f"Incremental transformed data saved to {parquet_inc_path}")

# Section 4: Verification
verified_full = pd.read_parquet(parquet_full_path)
verified_inc = pd.read_parquet(parquet_inc_path)
print("Verified full data (first 5 rows):")
print(verified_full.head())
print("Verified incremental data (first 5 rows):")
print(verified_inc.head())

