# Quality-preserving Model for Electronics Production Quality Tests Reduction

## Overview
This repository contains the analysis code for the study:

**Quality-preserving Model for Electronics Production Quality Tests Reduction**  
Noufa Haneefa, Teddy Lazebnik, Einav Peretz-Andersson

The project proposes and evaluates an adaptive test-selection framework for high-volume electronics manufacturing that combines:
1. Offline minimum-cost diagnostic subset selection (greedy set cover).
2. Offline cost-risk trade-off analysis (Pareto frontier).
3. Online adaptation using a Thompson Sampling multi-armed bandit with process-stability monitoring.

The framework is evaluated on two production stages:
- FCT (Functional Circuit Test)
- EOL (End-of-Line Test)

## Repository Contents
This repository is notebook-centric. Each notebook corresponds to a research question (RQ) or validation phase.

- `rq1fct.ipynb`: FCT RQ1 analysis (minimum-cost subset / set-cover flow).
- `rq2fct.ipynb`: FCT RQ2 Pareto analysis and reduced plan construction.
- `rq3fct.ipynb`: FCT RQ3 adaptive online policy (bandit-based switching).
- `valfct.ipynb`: FCT temporal/validation evaluation.
- `rq1eol.ipynb`: EOL RQ1 analysis and preprocessing outputs.
- `rq2eol.ipynb`: EOL RQ2 Pareto analysis and reduced plan construction.
- `rq3eol.ipynb`: EOL RQ3 adaptive online policy (bandit-based switching).
- `eolval.ipynb`: EOL temporal/validation evaluation.

## Requirements
Recommended environment:
- Python 3.9+
- Jupyter Notebook or JupyterLab

Quick start files:
- `requirements.txt` for dependency installation
- `DATA_FORMAT.md` for dataset schema and pipeline artifacts

Python packages used in notebooks:
- `pandas`
- `numpy`
- `matplotlib`
- `scipy`

Install:

```bash
python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS/Linux
# source .venv/bin/activate

pip install pandas numpy matplotlib scipy notebook
```

## Data and Inputs
Raw production datasets are not included in this repository.

The notebooks expect CSV data with manufacturing step-level logs. Based on the implemented pipeline, required core columns include:
- `source_file` (unit/run identifier)
- `outcome_from_filename` (PASS/FAIL/ABORT-like unit outcome)
- `result` (step result)
- `step_name_1`, `step_name_2` (hierarchical step naming)
- `step_time` (step execution time)
- `no` (record index/order field)

Some notebooks currently use machine-local absolute input paths (for example `C:\FCT_EDA\...` or `C:\EOL_EDA\...`). Update these path variables before running.

## How to Run
Run notebooks top-to-bottom in this order.

### EOL pipeline
1. `rq1eol.ipynb`
2. `rq2eol.ipynb`
3. `rq3eol.ipynb`
4. `eolval.ipynb`

### FCT pipeline
1. Prepare/generate preprocessed FCT artifacts expected by the notebooks (`fct_cleaned.csv`, `fct_outcome_matrix.csv`, `fct_cost_vector.csv`, `fct_unit_summary.csv`).
2. `rq1fct.ipynb`
3. `rq2fct.ipynb`
4. `rq3fct.ipynb`
5. `valfct.ipynb`

## Main Generated Outputs
Typical outputs written by notebooks include:

### EOL outputs
- `eol_cleaned.csv`
- `eol_outcome_matrix.csv`
- `eol_cost_vector.csv`
- `eol_unit_summary.csv`
- `eol_step_summary.csv`
- `eol_rq1_c_star.csv`
- `eol_rq1_non_diagnostic.csv`
- `eol_rq1_summary.csv`
- `eol_rq2_cred.csv`
- `eol_rq2_pareto_results.csv`
- `eol_results_comparison.csv`
- `eol_mab_log.csv`
- `eol_val_final_results.csv`

### FCT outputs
- `fct_cost_vector.csv`
- `fct_rq1_c_star.csv`
- `fct_rq2_cred.csv`
- `fct_rq2_pareto.csv`
- `fct_rq2_summary.csv`
- `fct_results_comparison.csv`
- `fct_mab_log.csv`
- `fct_val_sensitivity.csv`
- `fct_val_final_results.csv`

## Reproducibility Notes
- Notebook execution depends on prior generated CSV artifacts; run in pipeline order.
- If you re-run from scratch, clear stale intermediate files to avoid mixing versions.
- Keep random seeds/configuration fixed inside notebooks when comparing runs.
- The adaptive policy behavior depends on temporal ordering of units; do not shuffle validation sequences.

## Citation
If you use this repository, please cite the study:

```bibtex
@article{haneefa2026quality,
  title   = {Quality-preserving Model for Electronics Production Quality Tests Reduction},
  author  = {Haneefa, Noufa and Lazebnik, Teddy and Peretz-Andersson, Einav},
  journal = {Manuscript in preparation / submitted},
  year    = {2026}
}
```

## Contact
Corresponding author: `hano24vi@student.ju.se`
