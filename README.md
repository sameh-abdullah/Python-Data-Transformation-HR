# 🧹 Employee Data Cleaning & Transformation ETL Pipeline

## 📝 Overview

This project demonstrates an ETL (Extract, Transform, Load) pipeline implemented in Python jupyter notebook for cleaning, standardizing, and enriching employee data from the csv source file.

The pipeline applies multiple data quality operations including:

- ✨ Data standardization
- 🧼 String cleaning
- 🔄 Type conversion
- 🚫 Missing value imputation
- 🧬 Feature engineering
- 📊 Data normalization
- ✅ Data validation

The final dataset is prepared for:
- 📈 Analytics
- 📄 Reporting
- 📊 Dashboarding
- 🏬 Data warehousing
- 🤖 Machine learning preprocessing

---

# Architecture

```text
csv file (Raw Data)
        ↓
Data Cleaning & Standardization
        ↓
Feature Engineering
        ↓
Missing Value Imputation (KNN algorithm)
        ↓
csv file (Cleaned Data)
```

---

# Source Table

```csv file
Messy_Employee_dataset.csv
```

The source table contains raw employee records with inconsistent formatting, missing values, and non-standardized attributes.

---

# Final Output Columns(Data Catalog)

| Column | Description |
|---|---|
| Employee_ID | Employee identifier (exe. EMP1000) |
| First_Name | Employee first name |
| Last_Name | employee last name |
| Age | Employee age  |
| Department | Department where the employee works |
| Region | Region where the employee works |
| Is_Active | if the employee currently work or not (exe 1, 0) |
| Join_Date | Data when the employee is join the company |
| Salary | the salary amount will the staff receive |
| Email | work email |
| Phone | employee phone number |
| Performance_Score | The performance score of employee (exe Excellent, Good, Poor, Average)|
| Remote_Work | the modality work remote or inperson (exe. 1, 0) |
| duplicate_email_flag | Flage the duplication email for the data check with the provider (exe. True, False) |

---

# Data Quality Improvements Achieved

✅ Standardized text values  
✅ Removed extra spaces  
✅ Converted invalid values safely  
✅ Handled missing values  
✅ Normalized categorical fields  
✅ Created analytical dimensions  
✅ Prevented ETL runtime failures  
✅ Improved reporting readiness  

---

# Use Cases

This ETL pipeline is suitable for:

- HR analytics
- Power BI dashboards
- Workforce reporting
- Data warehouse staging
- Machine learning preprocessing
- Data quality assessment

---

# Author

**Sameh Abdullah**  
**LinkedIn**: [My Profile](https://linkedin.com/in/sameh-abdullah-961554176)
