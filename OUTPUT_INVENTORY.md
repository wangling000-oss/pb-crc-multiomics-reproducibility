# OUTPUT_INVENTORY

This file provides an inventory of the regenerated outputs in the reproducibility package, including which script generates which output file and how each output relates to the manuscript.

## Root-level entry point

The root-level script `run_all.sh` runs the main directly executable workflows currently standardized for:
- `1.NHANES/`
- `3.Machine learning/01_main_reproducible_pipeline/`
- `5.MR/`

Outputs remain stored in their respective module-level directories as described below.

## 1. NHANES module

### Main workflow

#### 1.1 Data preparation and analytic dataset construction

**Purpose:**  
Prepare the NHANES analytic dataset used in the manuscript, including variable cleaning, recoding, and derivation of the colorectal cancer outcome and blood lead exposure variables.

**Main inputs:**  
- Public NHANES source files used in the reproducibility package  
- Merged NHANES analysis data prepared according to the manuscript workflow

**Generated outputs:**  
- Cleaned NHANES analytic dataset used for descriptive statistics and regression analyses  
- Flowchart-related summary tables documenting sample selection

**Notes:**  
This step prepares the unified dataset used for Table 1, Table 2, and the NHANES-related flowchart.

#### 1.2 Descriptive statistics and Table 1

**Purpose:**  
Generate the weighted descriptive baseline table for the analytic sample.

**Main inputs:**  
- Cleaned NHANES analytic dataset  
- Survey design object constructed using PSU, strata, and MEC weights

**Generated outputs:**  
- `Table1.csv` or equivalent baseline table output  
- Formatted Table 1 outputs retained in the package

**Notes:**  
This step supports the manuscript baseline characteristics table and uses survey-design-aware summary procedures consistent with the revised manuscript description.

#### 1.3 Survey-weighted regression and Table 2

**Purpose:**  
Run the survey-weighted logistic regression models for the association between blood lead and colorectal cancer.

**Main inputs:**  
- Cleaned NHANES analytic dataset  
- Survey design object constructed using PSU, strata, and MEC weights

**Generated outputs:**  
- `Table2.csv` or equivalent regression result table  
- Model-specific regression outputs for the manuscript

**Notes:**  
These outputs correspond to the main NHANES regression analyses reported in the manuscript and are generated using survey-design-aware methods.

#### 1.4 Flowchart outputs

**Purpose:**  
Document the participant inclusion and exclusion process for the NHANES analysis.

**Main inputs:**  
- Cleaned NHANES analytic dataset  
- Flow-summary counts generated during data preparation

**Generated outputs:**  
- NHANES flowchart summary table(s)  
- Flowchart figure or flowchart input tables retained in the package

**Notes:**  
These outputs support the NHANES sample-selection figure and document the derivation of the final analytic sample.

### Summary table

| Workflow component | Main output files | Role in manuscript |
|---|---|---|
| Data preparation | cleaned analytic dataset, flow summary tables | Prepares the NHANES analysis sample |
| Descriptive statistics | Table 1 output files | Supports manuscript Table 1 |
| Survey-weighted regression | Table 2 output files | Supports manuscript Table 2 |
| Flowchart generation | flowchart summary files / figure inputs | Supports NHANES sample-selection figure |

### Relationship to the manuscript

The outputs in this module support the NHANES component of the manuscript, including the analytic sample derivation, weighted descriptive statistics, and survey-weighted regression analyses.

---

## 2. GEO module

### Public input data

- GEO accession used in this module: `GSE74602`  
- Public GEO-derived expression data used for downstream differential-expression analysis  
- Downstream candidate-gene visualization inputs retained in the package

### Main workflow

#### 2.1 GEO data acquisition and preprocessing

**Purpose:**  
Retrieve the GEO dataset and prepare the expression matrix and sample grouping information for downstream differential-expression analysis.

**Main inputs:**  
- Public GEO dataset `GSE74602`

**Generated outputs:**  
- Processed GEO expression matrix  
- Sample annotation / grouping files used in downstream analysis

**Notes:**  
This step prepares the standardized GEO input used for reproducible downstream analyses.

#### 2.2 Differential-expression analysis

**Purpose:**  
Perform differential-expression analysis between the predefined comparison groups.

**Main inputs:**  
- Processed GEO expression matrix  
- Sample grouping information

**Generated outputs:**  
- Differential-expression result table  
- DEG summary files retained in the package  
- Volcano-plot source table  
- Heatmap source table, where applicable

**Notes:**  
These outputs support the GEO-derived candidate-gene screening results described in the manuscript.

#### 2.3 Candidate-gene expression visualization

**Purpose:**  
Generate visualization tables and plots for selected candidate genes based on the processed GEO expression data.

**Main inputs:**  
- Processed GEO expression matrix  
- Selected candidate-gene list

**Generated outputs:**  
- Candidate-gene expression table(s)  
- Boxplot source table(s)  
- Figure-ready visualization outputs retained in the package

**Notes:**  
These outputs support the GEO visualization panels and document the data underlying the selected candidate-gene plots.

### Summary table

| Workflow component | Main output files | Role in manuscript |
|---|---|---|
| GEO acquisition and preprocessing | processed expression matrix, grouping files | Prepares GEO input for downstream analysis |
| Differential-expression analysis | DEG result tables, volcano/heatmap source tables | Supports GEO screening results |
| Candidate-gene visualization | expression tables, boxplot source tables, figure outputs | Supports GEO expression figure panels |

### Relationship to the manuscript

The outputs in this module support the GEO component of the manuscript, including data preprocessing, differential-expression analysis, and selected candidate-gene visualization.

---

## 3. Machine-learning module

### Core input files

- `ml_input_matrix.csv`  
- `ml_labels.csv`  
- `reproducible_splits.rds`

### Main workflow

#### 3.1 `01_main_reproducible_pipeline/01_make_splits.R`

**Purpose:**  
Create or validate the predefined split structure used in the reproducible machine-learning workflow.

**Main inputs:**  
- `ml_input_matrix.csv`  
- `ml_labels.csv`  
- `reproducible_splits.rds`

**Generated outputs:**  
- `01_main_reproducible_pipeline/outputs/split_summary.csv`

#### 3.2 `01_main_reproducible_pipeline/02_run_nested_svm_rfe.R`

**Purpose:**  
Run the main nested cross-validation workflow with SVM-RFE, including feature selection, hyperparameter tuning, model fitting, and outer-fold prediction.

**Main inputs:**  
- `ml_input_matrix.csv`  
- `ml_labels.csv`  
- `reproducible_splits.rds`

**Generated outputs:**  
- `01_main_reproducible_pipeline/outputs/outer_fold_predictions.csv`  
- `01_main_reproducible_pipeline/outputs/selected_features_by_fold.csv`  
- `01_main_reproducible_pipeline/outputs/performance_summary.csv`  
- `01_main_reproducible_pipeline/outputs/performance_summary_overall.csv`

#### 3.3 `01_main_reproducible_pipeline/03_make_roc_from_outer_predictions.R`

**Purpose:**  
Generate ROC-related outputs from the outer-fold predictions obtained from the nested cross-validation workflow.

**Main inputs:**  
- `01_main_reproducible_pipeline/outputs/outer_fold_predictions.csv`

**Generated outputs:**  
- `01_main_reproducible_pipeline/outputs/roc_points_nested_cv.csv`  
- `01_main_reproducible_pipeline/outputs/auc_nested_cv.csv`  
- `01_main_reproducible_pipeline/outputs/roc_curve_nested_cv.pdf`

#### 3.4 `01_main_reproducible_pipeline/04_fit_final_nomogram.R`

**Purpose:**  
Fit the final model using the selected features and generate nomogram-related presentation outputs.

**Main inputs:**  
- `ml_input_matrix.csv`  
- `ml_labels.csv`  
- `01_main_reproducible_pipeline/outputs/selected_features_by_fold.csv`

**Generated outputs:**  
- `01_main_reproducible_pipeline/outputs/final_nomogram_feature_frequency.csv`  
- `01_main_reproducible_pipeline/outputs/final_nomogram_coefficients.csv`  
- `01_main_reproducible_pipeline/outputs/final_nomogram.pdf`  
- `01_main_reproducible_pipeline/outputs/final_calibration_plot.pdf`  
- `01_main_reproducible_pipeline/outputs/final_dca_plot.pdf`

#### 3.5 `01_main_reproducible_pipeline/run_all_pipeline.R`

**Purpose:**  
Wrapper script that executes the full main machine-learning pipeline in sequence.

**Generated outputs:**  
This script reproduces all machine-learning outputs listed above.

### Summary table

| Script | Main output files | Role in workflow |
|---|---|---|
| `01_make_splits.R` | `split_summary.csv` | Prepare or validate reproducible splits |
| `02_run_nested_svm_rfe.R` | `outer_fold_predictions.csv`, `selected_features_by_fold.csv`, `performance_summary.csv`, `performance_summary_overall.csv` | Main nested cross-validation analysis |
| `03_make_roc_from_outer_predictions.R` | `roc_points_nested_cv.csv`, `auc_nested_cv.csv`, `roc_curve_nested_cv.pdf` | Generate ROC-related outputs |
| `04_fit_final_nomogram.R` | `final_nomogram_feature_frequency.csv`, `final_nomogram_coefficients.csv`, `final_nomogram.pdf`, `final_calibration_plot.pdf`, `final_dca_plot.pdf` | Generate final model presentation outputs |
| `run_all_pipeline.R` | all outputs above | Run the full reproducible ML workflow |

### Relationship to the manuscript

The outputs in this module support the machine-learning component of the manuscript. The nested cross-validation outputs provide the primary reproducible performance estimates, whereas the nomogram-related outputs are presentation-oriented results derived from the final selected features.

---

## 4. Single-cell RNA sequencing and CellChat module

### Public input files

- `GSE144735.txt`  
- `GSE144735.csv`

### Main workflow

#### 4.1 `1.Reading single-cell files (csv).R`

**Purpose:**  
Read the public raw file and convert it into the CSV format used in the downstream workflow.

**Main input:**  
- `GSE144735.txt`

**Generated output:**  
- `GSE144735.csv`

#### 4.2 `2.Batch effect correction and dimensionality reduction.R`

**Purpose:**  
Perform preprocessing, batch effect correction, clustering, and dimensionality reduction.

**Main input:**  
- `GSE144735.csv`

**Generated output:**  
- Processed single-cell object used in the annotation step

#### 4.3 `3.Single-cell annotation/3.Single-cell annotation.R`

**Purpose:**  
Perform cell-type annotation and export the main source tables used for annotation-related visualizations.

**Generated outputs:**  
- `3.Single-cell annotation/af2025.rds`  
- `3.Single-cell annotation/yjsl_Type.rda`  
- `3.Single-cell annotation/umap_coordinates.csv`  
- `3.Single-cell annotation/annotation_dotplot_table.csv`  
- `3.Single-cell annotation/selected_gene_dotplot_table.csv`  
- `3.Single-cell annotation/featureplot_HMOX1_table.csv`

#### 4.4 `4.CellChat/4.CellChat.R`

**Purpose:**  
Perform CellChat analysis using the annotated single-cell object and export the source tables for CellChat visualization.

**Main input:**  
- `3.Single-cell annotation/yjsl_Type.rda`

**Generated outputs:**  
- `4.CellChat/cellchat.rda`  
- `4.CellChat/cellchat_group_size.csv`  
- `4.CellChat/cellchat_net_count.csv`  
- `4.CellChat/cellchat_net_weight.csv`

### Summary table

| Script | Main output files | Role in workflow |
|---|---|---|
| `1.Reading single-cell files (csv).R` | `GSE144735.csv` | Convert GEO supplementary text file into downstream analysis input |
| `2.Batch effect correction and dimensionality reduction.R` | processed single-cell object | Preprocessing, batch correction, clustering, and UMAP generation |
| `3.Single-cell annotation/3.Single-cell annotation.R` | `af2025.rds`, `yjsl_Type.rda`, `umap_coordinates.csv`, `annotation_dotplot_table.csv`, `selected_gene_dotplot_table.csv`, `featureplot_HMOX1_table.csv` | Cell-type annotation and export of annotation-related source tables |
| `4.CellChat/4.CellChat.R` | `cellchat.rda`, `cellchat_group_size.csv`, `cellchat_net_count.csv`, `cellchat_net_weight.csv` | Cell-cell communication analysis and export of CellChat source tables |

### Relationship to the manuscript

The outputs in this module support the scRNA-seq and CellChat components of the manuscript.

---

## 5. Mendelian randomization module

### Main input files

#### Exposure
- `data/exposure/eQTLgenp5e-08_kb_10000_r2_0.01.xlsx`  
- `data/exposure/symbol.csv`

#### Outcome
- `data/outcome/finngen_R10_C3_COLORECTAL_EXALLC.gz`

#### LD reference panel
- `resources/1kg.v3/EUR.bed`  
- `resources/1kg.v3/EUR.bim`  
- `resources/1kg.v3/EUR.fam`

### Main workflow

#### `scripts/mr_sensitivity.R`

**Purpose:**  
Run the main MR analysis, including instrument preparation, local LD clumping, harmonization, MR estimation, heterogeneity testing, pleiotropy testing, and HMOX1-focused LD sensitivity analysis.

**Generated outputs in `result/`:**  
- `MR_final_IV_SNP_list.csv`  
- `MR_result_eqtlgen.csv`  
- `MR_heterogeneity_eqtlgen.csv`  
- `MR_pleiotropy_eqtlgen.csv`  
- `Table_S4_LD_sensitivity_HMOX1.csv`

**Generated outputs in `plots/`:**  
- `scatter_ENSG00000100292.png`  
- `leaveoneout_ENSG00000100292.png`  
- `funnel_ENSG00000100292.png`

### Summary table

| Script | Main output files | Role in workflow |
|---|---|---|
| `scripts/mr_sensitivity.R` | `MR_final_IV_SNP_list.csv`, `MR_result_eqtlgen.csv`, `MR_heterogeneity_eqtlgen.csv`, `MR_pleiotropy_eqtlgen.csv`, `Table_S4_LD_sensitivity_HMOX1.csv`, `scatter_ENSG00000100292.png`, `leaveoneout_ENSG00000100292.png`, `funnel_ENSG00000100292.png` | Main MR analysis and HMOX1 sensitivity analysis |

### Relationship to the manuscript

The outputs in this module support the Mendelian randomization component of the manuscript.