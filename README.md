# GDSC-Drug-Sensitivity-Analysis
This project explores whether machine learning can identify patterns associated with drug sensitivity using pharmacogenomic screening data from the GDSC database.

This study ultimately aims to understand the dependcy on how the gene's of an individual with a tumor history affects the respons to the dug being injected

Dataset source link https://www.kaggle.com/datasets/samiraalipour/genomics-of-drug-sensitivity-in-cancer-gdsc

For better comprehension I have divided the dataset into  4 entities such as HOST,TREATMENT , MOLECULAR FINGERPRINT and TREATMENT_RESPONSE

**HOST** - This includes information such as the obtained CELL LINE , COSMIC ID, its GROWTH_PROPERTIES ,SCREENING_MEDIUM , GENOMIC_DRUG_SENSITIVITY_IN_CANCER_TISSUE_DESCRIPTOR_1&2 (1 broadly classifies the kind of tumor such as lung ,skin,etc. , 2 is the granular classification type such as carcinoma, melanoma etc),TCGA (The Cancer Genome Atlas) Classification

**TREATMENT** - These columns tell us about the chemical weapon being deployed against the cancer: DRUG_ID: The unique database barcode for the specific chemical compound00,DRUG_NAME,TARGET,TARGET_PATHWAY(e.g., "DNA replication" or "MAPK signaling").

**The Molecular Fingerprint** - LN_IC50 (Natural Log of IC50:IC_{50} is the concentration of the drug required to kill exactly 50% of the cancer cells.),AUC (Area Under the Curve),Z_SCORE (standardized drug response)

# Technologies Used

- Python
- Pandas
- NumPy
- SciPy
- Scikit-learn
- Matplotlib
- Jupyter Notebook

  # Machine Learning Models

The following machine learning models were implemented throughout the project:

| Model | Purpose |
|---------|---------|
| Linear Regression | Study relationships between continuous drug response variables |
| Logistic Regression | Predict drug sensitivity vs resistance |
| Decision Tree | Interpret biological decision rules associated with drug response |


# Project Workflow

Raw Dataset
      ↓
Data Cleaning
      ↓
Exploratory Data Analysis
      ↓
Statistical Analysis
      ↓
Regression Analysis
      ↓
Classification Models
      ↓
Decision Tree Interpretation
      ↓
Biological Insights


