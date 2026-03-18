# MANIFEST

This file lists the main files and directories included in the reproducibility package.

 `run_all.sh`: Root-level entry-point script for the main directly executable workflows.
## Root-level files

- `README.md` — main overview of the reproducibility package
- `MANIFEST.md` — inventory of the main files and directories in the package
- `OUTPUT_INVENTORY.md` — mapping of scripts to regenerated outputs across modules

---

## 1. NHANES

Directory: `1.NHANES/`

Main files:

- `1.NHANES/README.md` — module-level instructions for the NHANES workflow
- `1.NHANES/NHANES.R` — main NHANES analysis script
- `1.NHANES/NHANES_run_log.txt` — retained run log for the NHANES workflow
- `1.NHANES/sessionInfo.txt` — session information for the NHANES workflow
- `1.NHANES/NHANES_flowchart_counts.csv` — flowchart count summary for sample selection
- `1.NHANES/Supplement_missing_counts.csv` — supplementary missing-data summary
- `1.NHANES/Table1_weighted_CRC_vs_nonCRC_flow.docx` — formatted Table 1 output
- `1.NHANES/Table2_Model1_weighted.csv` — weighted regression results for Model 1
- `1.NHANES/Table2_Model2_weighted.csv` — weighted regression results for Model 2
- `1.NHANES/Table2_Model3_weighted.csv` — weighted regression results for Model 3
- `1.NHANES/Table2_PforTrend_weighted.csv` — weighted trend test results
- `1.NHANES/Sensitivity_weighted_model3.csv` — weighted sensitivity analysis for Model 3
- `1.NHANES/Sensitivity_unweighted_model3.csv` — unweighted sensitivity analysis for Model 3
- `1.NHANES/Sensitivity_model3_unknown_category.csv` — sensitivity analysis with unknown-category handling

Notes:

- This directory contains the NHANES analytic workflow, regenerated regression tables, flowchart-related outputs, and reproducibility documentation retained for this module.

---

## 2. GEO

Directory: `2.GEO/`

Main files and directories:

- `2.GEO/README.md` — module-level instructions for the GEO workflow
- `2.GEO/1.Download GEO database data.R` — script for GEO data download and initial preparation
- `2.GEO/input/74602/` — input files related to GSE74602
- `2.GEO/input/110223/` — additional retained GEO-related input files
- `2.GEO/2.Differential analysis/2.Differential analysis.R` — differential-expression analysis script
- `2.GEO/2.Differential analysis/input/` — retained inputs for the differential-expression workflow
- `2.GEO/2.Differential analysis/output/DE.txt` — differential-expression result table
- `2.GEO/2.Differential analysis/output/DE_exp.txt` — expression table used in downstream visualization
- `2.GEO/2.Differential analysis/output/DEGS.txt` — retained DEG summary table
- `2.GEO/2.Differential analysis/output/DEGS_exp.txt` — DEG expression table used in downstream analyses
- `2.GEO/3.Volcano map/` — files related to volcano-plot generation
- `2.GEO/4.Heat map/4.Heat map.R` — heatmap generation script
- `2.GEO/4.Heat map/DEGS_exp.txt` — heatmap input table
- `2.GEO/5.Correlation heat map.R` — correlation heatmap script
- `2.GEO/6.KEGG and GO.R` — KEGG/GO enrichment script

Notes:

- This directory contains the GEO preprocessing, differential-expression analysis, and downstream visualization/enrichment scripts and retained input/output tables.

---

## 3. Machine learning

Directory: `3.Machine learning/`

Main files:

- `3.Machine learning/README.md` — module-level instructions for the machine-learning workflow
- `3.Machine learning/ml_input_matrix.csv` — canonical machine-learning input matrix
- `3.Machine learning/ml_labels.csv` — machine-learning sample labels
- `3.Machine learning/reproducible_splits.rds` — predefined reproducible split indices

Main workflow directory:

- `3.Machine learning/01_main_reproducible_pipeline/` — primary reproducible machine-learning workflow
  - `01_make_splits.R`
  - `02_run_nested_svm_rfe.R`
  - `03_make_roc_from_outer_predictions.R`
  - `04_fit_final_nomogram.R`
  - `run_all_pipeline.R`
  - `inputs/`
  - `outputs/`

Legacy directories retained for transparency:

- `3.Machine learning/02_legacy_rf_importance/` — legacy random forest importance materials
- `3.Machine learning/03_legacy_svm_screening/` — legacy SVM screening materials
- `3.Machine learning/04_legacy_single_gene_roc/` — legacy single-gene ROC materials
- `3.Machine learning/05_legacy_nomogram_visualization/` — legacy nomogram visualization materials

Notes:

- This directory contains both the revised main reproducible machine-learning pipeline and legacy materials retained for transparency and archival reference.

---

## 4. Single-cell RNA sequencing

Directory: `4.Single-cell RNA sequencing/`

Main files:

- `4.Single-cell RNA sequencing/README.md` — module-level instructions for the scRNA-seq and CellChat workflow
- `4.Single-cell RNA sequencing/GSE144735.txt` — downloaded public supplementary input file
- `4.Single-cell RNA sequencing/GSE144735.csv` — converted CSV file used in downstream analysis
- `4.Single-cell RNA sequencing/1.Reading single-cell files (csv).R` — conversion script for the public input file
- `4.Single-cell RNA sequencing/2.Batch effect correction and dimensionality reduction.R` — preprocessing and dimensionality-reduction script

Single-cell annotation directory:

- `4.Single-cell RNA sequencing/3.Single-cell annotation/`
  - `3.Single-cell annotation.R` — cell-type annotation script
  - `af2025.rds` — processed single-cell object
  - `yjsl_Type.rda` — annotated single-cell object
  - `umap_coordinates.csv` — saved UMAP coordinate table
  - `annotation_dotplot_table.csv` — annotation dot-plot source table
  - `selected_gene_dotplot_table.csv` — selected-gene dot-plot source table
  - `featureplot_HMOX1_table.csv` — HMOX1 feature-plot source table

CellChat directory:

- `4.Single-cell RNA sequencing/4.CellChat/`
  - `4.CellChat.R` — CellChat analysis script
  - `cellchat.rda` — saved CellChat object
  - `cellchat_group_size.csv` — CellChat group-size table
  - `cellchat_net_count.csv` — CellChat interaction-count table
  - `cellchat_net_weight.csv` — CellChat interaction-weight table

Notes:

- This directory contains the public input file, preprocessing scripts, annotation outputs, and CellChat outputs retained for the scRNA-seq workflow.

---

## 5. MR

Directory: `5.MR/`

Main files:

- `5.MR/README.md` — module-level instructions for the Mendelian randomization workflow

Exposure data:

- `5.MR/data/exposure/eQTLgenp5e-08_kb_10000_r2_0.01.xlsx` — exposure summary file
- `5.MR/data/exposure/symbol.csv` — gene-symbol mapping file

Outcome data:

- `5.MR/data/outcome/finngen_R10_C3_COLORECTAL_EXALLC.gz` — outcome GWAS summary statistics

Reference panel:

- `5.MR/resources/1kg.v3/` — retained LD reference panel directory
  - includes `EUR.bed`, `EUR.bim`, and `EUR.fam` files used for local LD clumping

Scripts:

- `5.MR/scripts/mr_sensitivity.R` — main MR analysis script

Notes:

- This directory contains the exposure and outcome summary statistics, LD reference panel, and the main MR script used for the Mendelian randomization workflow.