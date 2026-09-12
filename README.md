# Expert Rules for Lysosomal Storage Disorder Screening

Code and supporting results for the expert-rule component of the study:

> Rustamov J. et al., "Expert Rules Versus Machine Learning for Lysosomal Storage Disorder Identification: A Comparative Analysis Using Clinical Data," Scientific Reports (under review).

This repository contains the implementation and evaluation of a clinician-informed, rule-based screening approach for three lysosomal storage disorders:

- Gaucher disease
- Acid sphingomyelinase deficiency (ASMD)
- Saposin C deficiency

The expert-rule approach uses clinical features, laboratory measurements, and selected diagnostic information to identify patients who meet predefined screening criteria.

## Repository structure

```text
├── notebooks/
│   └── expert-rules-analysis.ipynb
│
├── results/
│   └── rule_based_evaluation_results.csv
│
├── data/
│   └── README.md
│
├── README.md
└── .gitignore
