# Intensity-persistence classes of NW Pacific tropical cyclones: analysis code and results

Code and complete output for the paper: "Tran, V. Q. and Dang, H. T. B. Intensity-Persistence Classes of Northwestern Pacific Tropical Cyclones and the Limits of Unsupervised Rapid-Intensification Discovery: A 48-Year Best-Track Analysis". Journal: Theoretical and Applied Climatology.

Release `v1.0-TAC`.

## Contents

| Path | Description |
|---|---|
| `paper_notebook.ipynb` | Full analysis pipeline. Reproduces every number, table and figure in the paper in a single pass. |
| `results/` | Output of one complete run of the notebook (see `results/00_environment.json` for software versions). |
| `results/RESULTS_SUMMARY.md` | Summary of all reported quantities. |
| `results/04_config_grid_full.csv` | Complete output of the 288-configuration HMM grid. |
| `results/figures/` | Figures 1–10 (PDF and PNG). |

Files in `results/` are numbered in the order of the notebook sections:

| File | Content |
|---|---|
| `01_data_diagnostics.json` | Dataset size, temporal grid, RI base rate, data partition |
| `02_kalman_sensitivity.csv` | Sensitivity to Kalman noise variances Q and R |
| `03_quantisation*.{json,csv}` | Quantisation statistics and the representative K = 6 fit |
| `04_config_grid_*.csv` | Configuration grid (full and aggregated) |
| `05_*` | Two-state model: class statistics (Table 1), transition matrix, dwell times |
| `06_*` | Intensity threshold (Table 2) and conditional tests (Table 3) |
| `07_*` | Monthly and annual class composition |
| `08_env_ks.csv` | Environmental separation (Table 5) |
| `09_higher_K.csv` | Higher-state wind-only models |
| `10_precursor.csv` | Pre-RI class distribution (Table 4) |
| `11_*` | Supervised baselines (Table 6) and leakage diagnostics |
| `12_epoch_sensitivity.csv` | Epoch sensitivity |
| `13_case_studies.csv` | Case studies |
| `14_*` | Supplementary diagnostics quoted in the text |

## Input data

The notebook expects two CSV files containing the JMA RSMC Tokyo best-track record for 1977–2024 with co-located ERA5 and ORAS5 fields, placed in the same directory as the notebook:

- `project_dataset_part1.csv`
- `project_dataset_part2.csv`

These files are not included in this repository. The underlying data are publicly available:

- JMA best track: https://www.jma.go.jp/jma/jma-eng/jma-center/rsmc-hp-pub-eg/trackarchives.html
- ERA5 and ORAS5: Copernicus Climate Change Service Climate Data Store, https://cds.climate.copernicus.eu

## Running

```bash
pip install numpy==1.26.4 pandas==2.2.3 scikit-learn==1.6.1 hmmlearn==0.3.3 scipy joblib matplotlib
jupyter nbconvert --to notebook --execute paper_notebook.ipynb
```

The run takes about 90 minutes on 24 CPU cores and is dominated by the 288-configuration grid. All random seeds are fixed. The two-state model and all statistical tests reproduce exactly across machines. Fits of the larger multivariate models can differ marginally between machines, because the EM algorithm is not reproducible bit-for-bit across hardware and BLAS libraries (for example, one observation in the representative K = 6 fit).

## Citation

If you use this code, please cite the paper above.

## Contact

Hong T. B. Dang (corresponding author), dangthibichhong@iuh.edu.vn
