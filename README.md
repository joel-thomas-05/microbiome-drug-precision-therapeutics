# OMBPT

# Oral Microbiome Precision Therapeutics

This repository contains a machine learning workflow for analyzing oral microbiome species abundance data and prioritizing drug-like compounds for potential therapeutic screening.

## Project Overview

The project combines two datasets:

1. **Oral microbiome abundance data**  
   Species-level bacterial abundance across multiple oral microbiome samples.

2. **Drug feature library**  
   A synthetic library of 5,000 compounds with physicochemical features such as solubility, permeability, bioavailability, pKa, molecular mass, and polarity.

The goal is to identify a bacterial species of interest from the oral microbiome dataset and use supervised machine learning to rank drug candidates based on predicted category.


## Methods

### 1. Microbiome Analysis

The microbiome table is cleaned by renaming taxonomy columns and converting sample read counts into numeric values. Species are grouped and ranked using:

- Total reads across samples
- Mean reads across samples
- Maximum reads in any sample
- Number of samples where the species is present

The most abundant species is selected as a simple candidate bacterial target for downstream therapeutic prioritization.

### 2. Drug Candidate Modeling

The drug library is modeled using the following features:

- Solubility
- Permeability
- Bioavailability
- pKa
- Molecular mass
- Polarity proxy

The target variable is the compound `Category`.

### 3. Machine Learning Models

Several models are compared:

- Logistic Regression
- Decision Tree
- Random Forest
- Gradient Boosting
- K-Nearest Neighbors
- Support Vector Machine

Models are evaluated with:

- Accuracy
- Macro F1-score
- Weighted F1-score
- Confusion matrix

### 4. Confidence Interval Model Comparison

To make the model comparison more reliable, the notebook uses repeated stratified train/test splits. Mean accuracy is plotted with a transparent 95% confidence interval band.

This helps show both average model performance and variability across splits.

### 5. Candidate Ranking

The best-performing model is trained on the full dataset and used to rank compounds by predicted probability of belonging to the highest-priority category.

The final output is:

```text
outputs/top_100_drug_candidates.csv
```

## How to Run

1. Open the notebook in Google Colab or Jupyter Notebook.
2. Place the input Excel files in the expected location.
3. Update the paths in Cell 2 if needed.
4. Run the notebook from top to bottom.



## Important Note

This project is a computational screening workflow. The ranked compounds are not validated treatments. Any candidate would require experimental testing, biological validation, and safety evaluation before therapeutic use.

## Skills Demonstrated

- Python data cleaning
- Pandas data analysis
- Microbiome abundance summarization
- Supervised machine learning
- Model comparison
- Confidence interval visualization
- Drug candidate ranking
