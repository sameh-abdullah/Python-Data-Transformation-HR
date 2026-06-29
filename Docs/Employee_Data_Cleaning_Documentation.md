# Employee Data Cleaning & Transformation ETL Pipeline

## Overview
This document summarizes the data cleaning and transformation process implemented in the notebook for employee data. The workflow covers loading data from a CSV file, inspecting its quality, cleaning and standardizing columns, and preparing the dataset for further analysis or reporting.

## Project Goal
The main objective of this notebook is to transform row employee data into a cleaner, more consistent dataset by:
- standardizing column names
- fixing inconsistent values
- converting data types
- handling missing values
- detecting duplicate values
- preparing the final dataset for downstream use

## Tools and Libraries Used
The notebook uses the following Python libraries:
- pandas for data manipulation and analysis
- numpy for numerical operations
- datetime for date handling
- sklearn for missing value imputation using KNNImputer

## Data Source
The primary input file used in the notebook is:
- Dataset/Messy_Employee_dataset.csv

## Step-by-Step Process

### 1. Import Required Libraries
The notebook begins by importing the main libraries needed for data processing:
- pandas as pd
- numpy as np
- datetime as dt

### 2. Load the Employee Dataset
The CSV file is read into a pandas DataFrame using:
```python
data_url = r'.\Dataset/Messy_Employee_dataset.csv'
employees_df = pd.read_csv(data_url)
```

### 3. Inspect the Dataset
The notebook uses the following command to inspect the structure of the dataset:
```python
employees_df.info()
```
This helps identify:
- column names
- data types
- missing values

### 4. Clean Column Names
Column names are standardized by trimming spaces and converting them to lowercase:
```python
cols = employees_df.columns.str.strip().str.lower()
employees_df.columns = cols
```

### 5. Standardize Employee ID Values
The employee ID column is converted to uppercase to keep values consistent:
```python
employees_df.employee_id = employees_df['employee_id'].str.upper()
```

### 6. Clean Name Fields
Leading and trailing spaces are removed, and the names are capitalized:
```python
name = ['first_name', 'last_name']
for col in name:
    employees_df[col] = employees_df[col].str.strip().str.capitalize()
```

### 7. Split Department and Region
The combined department_region field is split into two separate columns:
- department
- region

Example:
- IT-NorthAmerica becomes:
  - department = IT
  - region = NorthAmerica

```python
employees_df['department'] = (
    employees_df['department_region'].astype(str).str.split('-').str[0].str.capitalize()
)
employees_df['region'] = (
    employees_df['department_region'].astype(str).str.split('-').str[1].str.capitalize()
)
```

### 8. Standardize Employment Status
The employment status values are converted into a binary-style format:
- 1 = Active
- 0 = Inactive / Pending

```python
employees_df['status'] = employees_df['status'].apply(
    lambda x: 1 if str.lower(x) in ['active', 'pending'] else 0
)
```

### 9. Convert Join Date to Date Format
The join_date column is converted to datetime format:
```python
employees_df['join_date'] = pd.to_datetime(employees_df['join_date'])
```

### 10. Check Email Quality and Duplicates
Email values are trimmed, and duplicate email addresses are identified. A new flag column is created to mark duplicate emails:
```python
employees_df['email'] = employees_df['email'].str.strip()
employees_df['duplicate_email_flag'] = employees_df['email'].duplicated()
```

### 11. Clean Phone Numbers
Phone numbers are treated as identifiers rather than numeric values. Hyphens are removed and the values are converted to numeric form:
```python
employees_df['phone'] = pd.to_numeric(employees_df['phone'].astype(str).str.replace('-', ''))
```

### 12. Standardize Performance Scores
Performance scores are standardized to a consistent format using capitalization:
```python
employees_df['performance_score'] = employees_df['performance_score'].str.capitalize()
```

### 13. Convert Remote Work to Integer
The remote_work column is converted to integers for better data performance:
```python
employees_df['remote_work'] = employees_df['remote_work'].astype(int)
```

### 14. Handle Missing Values with KNN Imputation
Missing values in the age and salary columns are filled using the KNNImputer algorithm from sklearn.

```python
from sklearn.impute import KNNImputer

imputer = KNNImputer(n_neighbors=5, weights='distance')
df_imputed = imputer.fit_transform(numeric_df)
```

This method uses neighboring values to estimate and fill missing entries.

### 15. Reorder and Finalize the Dataset
The final DataFrame is reordered into a preferred column sequence and unnecessary columns are removed by selection:
```python
desire_columns_order = [
    'employee_id', 'first_name', 'last_name', 'age', 'region', 'department',
    'join_date', 'salary', 'email', 'phone', 'status', 'performance_score',
    'remote_work', 'duplicate_email_flag'
]
employees_df = employees_df.reindex(columns=desire_columns_order)
```

### 16. Convert Age to Integer
The age column is cast to integer type:
```python
employees_df['age'] = employees_df['age'].astype(int)
```

## Result
At the end of the workflow, the employee dataset is cleaned, standardized, and prepared for further analysis, reporting, or machine learning tasks.
