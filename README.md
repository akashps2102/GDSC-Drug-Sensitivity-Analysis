# GDSC-Drug-Sensitivity-Analysis
This project explores whether machine learning can identify patterns associated with drug sensitivity using pharmacogenomic screening data from the GDSC database.

This study ultimately aims to understand the dependcy on how the gene's of an individual with a tumor history affects the respons to the dug being injected

**Dataset** source link https://www.kaggle.com/datasets/samiraalipour/genomics-of-drug-sensitivity-in-cancer-gdsc

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



This is much better than I expected. You've gone beyond just applying algorithms—you've started asking biologically relevant questions. However, there are a few places where the interpretation should be more careful. Below is how I would present each section in a GitHub notebook or README.

---

# 1. Dataset Composition Analysis

## Objective

To understand the composition of the GDSC pharmacogenomic dataset before performing predictive modeling.

### Findings

* The **urogenital system** was the most represented tissue group (**605 samples**).
* Within the urogenital system, **ovarian cancer** was the most represented subtype (**255 samples**).
* **Large intestine** tumors contained the highest number of **MSI-H (Microsatellite Instability-High)** samples.
* Nearly every record contained information for **Copy Number Alteration (CNA)**, indicating extensive genomic profiling.
* The cleaned dataset contained:

  * **9 anti-cancer drugs**
  * **17 tissue groups**
  * **8 molecular targets**
  * **751 unique cancer cell lines**
* **Camptothecin** appeared to be the most frequently screened drug across most tissue groups.

### Scientific Interpretation

The dataset represents a diverse collection of cancer cell lines spanning multiple tissue origins and molecular targets. However, tissue representation is not uniform. The larger representation of urogenital cancers may influence downstream statistical analyses and predictive models by providing more training examples for this tissue type. Similarly, the frequent occurrence of Camptothecin suggests that it serves as one of the primary reference compounds within this subset of the dataset.

### Limitation

These observations describe the composition of the experimental dataset and **should not be interpreted as reflecting the real-world prevalence of these cancers or drugs.**

---

# 2. Distribution of Drug Response Variables

## Objective

To understand the statistical distribution of the three primary drug response measurements.

### Findings

| Variable | Skewness | Interpretation          |
| -------- | -------- | ----------------------- |
| LN_IC50  | -0.21    | Approximately symmetric |
| AUC      | -1.44    | Strong negative skew    |
| Z-score  | -0.02    | Nearly symmetric        |

### Scientific Interpretation

Both LN_IC50 and Z-score exhibit approximately symmetric distributions, making them suitable for regression modeling without substantial transformation. In contrast, the AUC distribution is negatively skewed, indicating that a larger proportion of observations have relatively high treatment responses, with fewer observations exhibiting low response values.

---

# 3. Relationship Between Drug Response Variables

## Objective

To quantify the relationships among the three principal drug response measurements.

---

### LN_IC50 → AUC

**Model Results**

* Coefficient = **0.03**
* R² = **0.53**

### Interpretation

Approximately **53% of the variation in AUC** can be explained using LN_IC50 alone, suggesting a **moderate positive relationship** between drug potency and overall treatment response.

---

### LN_IC50 → Z-score

**Model Results**

* Coefficient = **0.15**
* R² = **0.28**

### Interpretation

LN_IC50 explains only **28%** of the variability in standardized drug response (Z-score), indicating that additional biological factors contribute substantially to treatment sensitivity.

---

### AUC → Z-score

**Model Results**

* Coefficient = **5.15**
* R² = **0.52**

### Interpretation

AUC and Z-score demonstrate a moderate linear relationship, suggesting that both metrics capture related aspects of drug response while still providing complementary information.

---

# 4. Predicting Drug Potency (LN_IC50)

## Objective

To investigate whether biological characteristics of cancer cells can predict drug potency.

### Features Used

* Drug Name
* Tissue Type
* Cancer Subtype
* Drug Target
* Target Pathway
* MSI Status
* Growth Properties

### Results

| Dataset  | R²    |
| -------- | ----- |
| Training | 0.761 |
| Testing  | 0.749 |

### Interpretation

The similar training and testing performance indicates **good model generalization** with minimal evidence of overfitting. Approximately **75% of the variability in LN_IC50** can be explained using the selected biological features, suggesting that these characteristics collectively capture much of the information associated with drug potency.

---

# 5. Camptothecin Response Prediction

## Objective

To predict whether cancer cell lines are sensitive or resistant to Camptothecin based on biological characteristics.

### Results

Training Accuracy

70.5%

Testing Accuracy

66.9%

Predicted sensitivity probability

64.7%

### Interpretation

The model demonstrates **moderate predictive performance**, suggesting that tissue characteristics, genomic status and drug target information contain useful information for predicting response to Camptothecin. However, prediction accuracy indicates that additional biological variables are likely required to improve discrimination between sensitive and resistant cell lines.

### Limitation

The sensitivity labels were generated using the dataset median of Z-score rather than experimentally validated clinical response thresholds. Therefore, the predictions represent **relative sensitivity within this dataset**, not clinical treatment outcomes.

---

# 6. Melanoma-specific Drug Response

## Objective

To investigate drug sensitivity specifically within melanoma-derived cancer cell lines.

### Results

Training Accuracy

78.1%

Testing Accuracy

61.5%

### Interpretation

Although the model performs reasonably well during training, the reduced testing accuracy suggests weaker generalization for melanoma samples. This may reflect increased biological heterogeneity among melanoma cell lines or limited sample size.

---

# 7. Predicting Drug Sensitivity Across Melanoma Drugs

Training Accuracy

77%

Testing Accuracy

71%

### Interpretation

Including drug identity alongside biological characteristics improved predictive performance compared with the previous melanoma-specific model. This suggests that both the administered drug and intrinsic biological properties jointly influence treatment response.

---

# 8. Decision Tree Analysis

## Objective

To construct an interpretable model capable of classifying drug sensitivity.

### Results

Accuracy

88%

Precision

88%

Recall

88%

F1 Score

88%

### Scientific Interpretation

The Decision Tree achieved the highest predictive performance among the implemented classification models while providing transparent decision rules. Unlike regression-based approaches, the tree explicitly identifies combinations of biological features that separate sensitive and resistant samples, making it easier to interpret which variables contribute most strongly to classification.

---

# Overall Conclusions

After analyzing the dataset, several key observations emerged:

* The GDSC dataset exhibits substantial biological diversity across tissues, drugs and molecular targets.
* Drug response metrics (LN_IC50, AUC and Z-score) show moderate statistical relationships but capture distinct aspects of treatment response.
* Biological features collectively explain approximately **75% of the variability in drug potency**, demonstrating their predictive value.
* Logistic Regression provided moderate classification performance for predicting drug sensitivity.
* Decision Trees achieved the strongest classification performance while maintaining model interpretability.
* Drug response prediction appears to depend on a combination of tissue origin, molecular targets, pathway information and genomic characteristics rather than any single biological factor.

