# AV-AM Descriptors — QSPR Modeling of Aliphatic Alcohol Properties

This repository contains the data and analysis code supporting the manuscript on predicting
physicochemical properties of aliphatic alcohols from Augmented Vertex-Adjacency Matrix (AV-AM)
molecular descriptors, using multiple linear regression (MLR) and an artificial neural network
(ANN). It is published to satisfy the manuscript's Data and Software Availability statement.

**Citation:** this repository accompanies a manuscript that is currently under review. Full
citation details (authors, journal, DOI) will be added here once the article is published.

## Contents

| File | Description |
|---|---|
| `Alcohol_Data.xlsx` | Raw data: literature-sourced physical property values for 66 aliphatic alcohols (sheet `All_Properties`), plus the AV-AM descriptor values for 6 independent descriptor groups (`CW-I_without_H`, `CW-II_without_H`, `CW-mix_without_H`, `CW-I_with_H`, `CW-II_with_H`, `CW-mix_with_H`), one sheet each. |
| `MLR_Analysis.ipynb` | Multiple linear regression (MLR) analysis for all 12 physical properties: VIF-based variable elimination, model fitting, leave-one-out cross-validation (LOOCV), and Y-randomization. |
| `ANN_Analysis_bp.ipynb` | Artificial neural network (ANN) analysis, restricted to the boiling point (bp) property: nested cross-validation (5-fold inner CV hyperparameter search inside an outer LOOCV loop, repeated across 10 fixed random seeds), Y-randomization, and Williams Plot / applicability domain analysis. |
| `Eta_Squared_Analysis.ipynb` | Supporting analysis: eta-squared (η²) structural-variance decomposition, used to justify restricting the ANN model to the bp property only. |
| `MLR_vs_ANN_Comparison_bp.ipynb` | Paired statistical comparison (Wilcoxon signed-rank test, paired t-test) of the MLR and ANN models for bp, both evaluated under true leave-one-out validation. |

## Requirements

Python 3.x with: `pandas`, `numpy`, `scikit-learn`, `scipy`, `statsmodels`, `matplotlib`,
`openpyxl`, and `python-docx` (used only for the optional Word-report-generation cells).

## How to run

1. Open any notebook in Jupyter.
2. Make sure `Alcohol_Data.xlsx` is in the same folder (or update the `EXCEL_PATH` /
   `excel_path` variable at the top of the notebook).
3. Run the cells in order, from top to bottom. The MLR notebook presents a menu to choose
   which of the 12 properties to analyze.

Note: the ANN notebook's full nested cross-validation (10 seeds × multiple hyperparameter
candidates) is computationally intensive and can take on the order of hours to run to
completion.

## Notes on reproducibility

- Column and sheet names in the Excel file (e.g. `All_Properties`, `Aliphatic Alcohol`,
  `CW-I_without_H`, `Solvent`, `Per(A)`) are referenced literally in the code — do not rename them
  if you edit this file, or update the corresponding constants at the top of each notebook.
- `Per(A)`, `A(2,1)`, `A(2,2)`, `tr(A)`, `epsilon(A)` are the AV-AM descriptor names (graph
  invariants: perimeter, trace components, etc.) and are kept as mathematical notation rather
  than translated.
- Each notebook also contains the code used to generate the corresponding Word (.docx) results
  report; the full result tables and figures are reported in the manuscript and its
  supplementary material.
