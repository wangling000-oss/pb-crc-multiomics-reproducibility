## Repository contents

Due to folder-upload limitations during repository setup, each analysis module is currently provided as a separate ZIP archive in this repository:

- `1.NHANES.zip`
- `2.GEO.zip`
- `3.Machine learning.zip`
- `4.Single-cell RNA sequencing.zip`
- `5.MR.zip`

After downloading the repository, please unzip these archives in the repository root directory before execution. The expected working structure after extraction is:

- `1.NHANES/`
- `2.GEO/`
- `3.Machine learning/`
- `4.Single-cell RNA sequencing/`
- `5.MR/`

The workflow can then be executed from the project root according to the instructions in this README and by using `run_all.sh` where applicable.
## Recommended execution from the project root
#Code availability
The source code for the reproducibility workflow is hosted in a public GitHub repository. To ensure versioned archiving, the exact release corresponding to this manuscript revision has been deposited in Zenodo and assigned a DOI. Large auxiliary files are not bundled in the main source-code archive unless required for execution; where applicable, their role and access instructions are described separately in the README.
A root-level entry-point script is provided for the main directly executable workflows:

```bash
bash run_all.sh
t present, this script runs the standardized root-level workflows for:
1.NHANES/
3.Machine learning/01_main_reproducible_pipeline/
5.MR/
Other modules are retained in the package with module-level instructions because they involve larger public input files, multi-step execution, or retained archival materials:
2.GEO/
4.Single-cell RNA sequencing/
6.Molecular_Docking/
Please refer to the corresponding module-level README.md files for those components.

# Reproducibility package

This repository contains the reproducibility package for the manuscript.  
The package is organized by analysis module and retains the main scripts, key input files, regenerated outputs, and module-level documentation required to trace the workflow.

## Clean-environment reproduction

To verify computational reproducibility, the deposited workflow was re-executed in a clean local R environment from the project root after removing hard-coded paths and `setwd()` calls from the main reproducible scripts where applicable. The test run was performed by following the module-level README instructions using the deposited reproducibility package together with the required public input files retained in the package or described in the documentation.

Execution logs and `sessionInfo()` files are provided for modules where available.

## Package structure

```text
.
├── 1.NHANES/
├── 2.GEO/
├── 3.Machine learning/
├── 4.Single-cell RNA sequencing/
├── 5.MR/
├── 6.Molecular_Docking/
├── MANIFEST.md
├── OUTPUT_INVENTORY.md
└── README.md
Root-level files
README.md
Main overview of the reproducibility package.
MANIFEST.md
Inventory of the major files and directories included in the package.
OUTPUT_INVENTORY.md
Mapping of scripts to regenerated outputs and their relationship to the manuscript.
General use
This package is organized by module. Each module contains its own scripts and, where applicable, a module-level README.md.
Please run commands from the project root unless otherwise noted.
Paths below are written exactly as they appear in the current package.
1. NHANES
Directory: 1.NHANES/
Main script:
1.NHANES/NHANES.R
This module reproduces the NHANES component of the manuscript, including weighted descriptive statistics, weighted regression models, flowchart-related counts, and sensitivity analyses.
Run from the project root:
Rscript 1.NHANES/NHANES.R > 1.NHANES/NHANES_run_log.txt 2>&1
Main retained outputs in 1.NHANES/ include:
Table1_weighted_CRC_vs_nonCRC_flow.docx
Table2_Model1_weighted.csv
Table2_Model2_weighted.csv
Table2_Model3_weighted.csv
Table2_PforTrend_weighted.csv
NHANES_flowchart_counts.csv
Supplement_missing_counts.csv
Sensitivity_unweighted_model3.csv
Sensitivity_weighted_model3.csv
Sensitivity_model3_unknown_category.csv
NHANES_run_log.txt
sessionInfo.txt
For additional notes, see:
1.NHANES/README.md
2. GEO
Directory: 2.GEO/
This module contains the GEO download/preprocessing, differential-expression analysis, and downstream visualization/enrichment scripts retained for the GEO component of the manuscript.
Main files and subdirectories include:
2.GEO/1.Download GEO database data
2.GEO/2.Differential analysis/
2.GEO/3.Volcano map/
2.GEO/4.Heat map/
2.GEO/5.Correlation heat map.R
2.GEO/6.KEGG and GO.R
Because this module is organized into several retained subfolders, please follow the module-specific instructions in:
2.GEO/README.md
Representative retained outputs include differential-expression result tables and downstream visualization inputs such as:
2.GEO/2.Differential analysis/output/DE.txt
2.GEO/2.Differential analysis/output/DE_exp.txt
2.GEO/2.Differential analysis/output/DEGS.txt
2.GEO/2.Differential analysis/output/DEGS_exp.txt
3. Machine learning
Directory: 3.Machine learning/
This module contains the revised primary reproducible machine-learning workflow together with legacy materials retained for transparency.
Main retained files:
3.Machine learning/ml_input_matrix.csv
3.Machine learning/ml_labels.csv
3.Machine learning/reproducible_splits.rds
Primary reproducible workflow directory:
3.Machine learning/01_main_reproducible_pipeline/
Main scripts in the primary pipeline:
01_make_splits.R
02_run_nested_svm_rfe.R
03_make_roc_from_outer_predictions.R
04_fit_final_nomogram.R
run_all_pipeline.R
Legacy directories retained for transparency:
3.Machine learning/02_legacy_rf_importance/
3.Machine learning/03_legacy_svm_screening/
3.Machine learning/04_legacy_single_gene_roc/
3.Machine learning/05_legacy_nomogram_visualization/
To run the main reproducible workflow from the project root:
Rscript "3.Machine learning/01_main_reproducible_pipeline/run_all_pipeline.R"
Main generated outputs are written under:
3.Machine learning/01_main_reproducible_pipeline/outputs/
These include:
split_summary.csv
outer_fold_predictions.csv
selected_features_by_fold.csv
performance_summary.csv
performance_summary_overall.csv
roc_points_nested_cv.csv
auc_nested_cv.csv
roc_curve_nested_cv.pdf
final_nomogram_feature_frequency.csv
final_nomogram_coefficients.csv
final_nomogram.pdf
final_calibration_plot.pdf
final_dca_plot.pdf
or details, see:
3.Machine learning/README.md
4. Single-cell RNA sequencing
Directory: 4.Single-cell RNA sequencing/
This module contains the public single-cell input file, preprocessing scripts, annotation outputs, and CellChat outputs used in the scRNA-seq component of the manuscript.
Main retained input files:
4.Single-cell RNA sequencing/GSE144735.txt
4.Single-cell RNA sequencing/GSE144735.csv
Main scripts:
4.Single-cell RNA sequencing/1.Reading single-cell files (csv).R
4.Single-cell RNA sequencing/2.Batch effect correction and dimensionality reduction.R
Annotation directory:
4.Single-cell RNA sequencing/3.Single-cell annotation/
Main files in the annotation directory:
3.Single-cell annotation.R
af2025.rds
yjsl_Type.rda
umap_coordinates.csv
annotation_dotplot_table.csv
selected_gene_dotplot_table.csv
featureplot_HMOX1_table.csv
CellChat directory:
4.Single-cell RNA sequencing/4.CellChat/
Main files in the CellChat directory:
4.CellChat.R
cellchat.rda
cellchat_group_size.csv
cellchat_net_count.csv
cellchat_net_weight.csv
Because this module contains multiple sequential scripts, please follow the module-specific instructions in:
4.Single-cell RNA sequencing/README.md
Representative workflow order:
1.Reading single-cell files (csv).R
2.Batch effect correction and dimensionality reduction.R
3.Single-cell annotation/3.Single-cell annotation.R
4.CellChat/4.CellChat.R
5. MR
Directory: 5.MR/
This module contains the exposure and outcome summary-statistic files, LD reference panel, and the main Mendelian randomization script.
Main data directories:
5.MR/data/exposure/
5.MR/data/outcome/
Main retained files include:
5.MR/data/exposure/eQTLgenp5e-08_kb_10000_r2_0.01.xlsx
5.MR/data/exposure/symbol.csv
5.MR/data/outcome/finngen_R10_C3_COLORECTAL_EXALLC.gz
LD reference panel:
5.MR/resources/1kg.v3/
Main script:
5.MR/scripts/mr_sensitivity.R
Run from the project root:
Rscript 5.MR/scripts/mr_sensitivity.R
According to the current package structure, the main MR outputs are generated in module-level output directories such as:
result/
plots/
Representative retained/generated outputs include:
MR_final_IV_SNP_list.csv
MR_result_eqtlgen.csv
MR_heterogeneity_eqtlgen.csv
MR_pleiotropy_eqtlgen.csv
Table_S4_LD_sensitivity_HMOX1.csv
scatter_ENSG00000100292.png
leaveoneout_ENSG00000100292.png
funnel_ENSG00000100292.png
For details, see:
5.MR/README.md
6. Molecular docking
Directory: 6.Molecular_Docking/
This directory contains the retained molecular docking materials archived for transparency and manuscript traceability.
Please refer to the files retained in this directory and any accompanying module-level notes for the docking-related materials used in the manuscript.
Recommended reading order
To understand the package contents and locate files efficiently, please read in the following order:
README.md
MANIFEST.md
OUTPUT_INVENTORY.md
otes on the current package structure
This deposited package retains the original module-based organization of the analysis files.
Accordingly, outputs are stored within their respective module directories rather than in a single global output directory. The file paths written in this README follow the current deposited directory structure.
Manuscript linkage
The modules in this package correspond to the major components of the manuscript:
1.NHANES/ → NHANES analysis
2.GEO/ → GEO differential-expression and enrichment analysis
3.Machine learning/ → machine-learning analysis
4.Single-cell RNA sequencing/ → scRNA-seq and CellChat analysis
5.MR/ → Mendelian randomization analysis
6.Molecular_Docking/ → molecular docking materials
For a more detailed script-to-output mapping, please see:
OUTPUT_INVENTORY.md
## Required input data and reconstruction of prepared inputs

All required input files currently retained in the package are placed in the corresponding module-level `input/` or data directories and are referenced by relative paths in the scripts.  
For files that cannot be redistributed directly, each module-level `README.md` specifies:  
(1) the exact public source,  
(2) dataset identifier and version/release,  
(3) the exact filename to download,  
(4) the directory where the file should be placed after download, and  
(5) the preprocessing scripts and execution order required to reconstruct the same prepared inputs using commands only.

Intermediate products generated during preprocessing and analysis are also retained where applicable and are described in the corresponding module-level `README.md` files and in `OUTPUT_INVENTORY.md`.