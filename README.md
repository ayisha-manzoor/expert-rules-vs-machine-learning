# Expert Rules for Lysosomal Storage Disorder Screening

This repository contains code and supporting results for the **expert-rule component** of the following study:

> **Rustamov J. et al.**  
> *Expert Rules Versus Machine Learning for Lysosomal Storage Disorder Identification: A Comparative Analysis Using Clinical Data.*  
> **Scientific Reports** (accepted, awaiting publication).

## Overview

This repository focuses on the clinician-informed, rule-based screening approach developed for identifying patients with selected lysosomal storage disorders.

The expert-rule analysis covers:

- Gaucher disease
- Acid sphingomyelinase deficiency (ASMD)
- Saposin C deficiency

The screening approach uses combinations of clinical findings, laboratory measurements, diagnostic information, and relevant medication history.

## Expert Rules

Five predefined expert rules are evaluated based on combinations of clinical and laboratory characteristics, including:

- Organomegaly
- Complete blood count (CBC) abnormalities
- Growth retardation
- Failure to thrive
- Height and weight centile information
- Interstitial lung disease
- Hypotonia
- Developmental delay
- Relevant medication history for determining appropriate laboratory values

A patient is classified as positive when at least one of the five expert rules is satisfied.

## Evaluation

The rule-based approach was evaluated using:

- Precision
- Recall
- F1 score
- F2 score
- Balanced Accuracy
- Number Needed to Screen (NNS)
- True Positives (TP)
- True Negatives (TN)
- False Positives (FP)
- False Negatives (FN)

Aggregate evaluation results are provided in:

`results/rule_based_evaluation_results.csv`

Additional rule-verification results are provided for:

- Gaucher disease
- ASMD

## Repository Structure

```text
expert-rules-vs-machine-learning/
│
├── notebooks/
│   ├── expert-rules-analysis.ipynb
│   └── gaucher-expert-rules.ipynb
│
├── results/
│   ├── rule_based_evaluation_results.csv
│   ├── gaucher_rule_verification_public.xlsx
│   └── asmd_rule_verification_public.xlsx
│
├── data/
│   └── README.md
│
├── README.md
└── .gitignore

Data Availability

The original patient-level clinical datasets are not included in this repository due to applicable privacy, institutional, and ethical restrictions.

The analysis was performed using clinical, laboratory, diagnostic, demographic, and medication data available to the research team.

Only supporting code and non-identifying analysis results are provided in this repository.
