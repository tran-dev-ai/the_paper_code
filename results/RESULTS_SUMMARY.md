# Reported quantities

Generated 2026-10-23 01:17:24 | hmmlearn 0.3.3 | seed 42 | Q=1.0 kt^2 | R=2.0833 kt^2


## Data

- Observations (MaxWind >= 35 kt): **28,156** from **1,220** storms
- Smallest reported non-missing wind: **35 kt**
- Duplicate timestamps removed: 92
- Time steps other than 6 h: **19.16%**
- RI labels, row offset: n=23,338, base 3.072%, 717 cases
- RI labels, timestamp match: n=21,876, base **3.364%**, 736 cases
- delta-V24 differs between conventions for **12.3%** of records
- train / valid / test = 22,580 / 3,196 / 2,380

## Quantisation

- delta-V6 exactly zero: **52.2%**
- delta-V24 exactly zero: 17.8%
- |delta-V6| < 0.5 kt after smoother 18.1%, after causal filter 22.9%
- K=6 (full covariance), 21,505 decoded observations: **1** fully absorbing state(s), **20.0%** of decoded observations; largest state n=11,296 with 60.8% zeros

## Configuration grid

- Configurations: **288**, converged 288
- Grid maximum per-state RI proportion: **13.55%** (base rate 3.36%)
- Maximum among numerically stable fits (kappa < 10000): **8.52%**
- Configurations at or above 10%: **6**, of which **6** are numerically singular
- Grid maximum attained by F4D_overlap, K=9, full covariance, kappa 2.50e+15

```
cov              diag   full
feature_set                 
F2D_nonoverlap   6.66   6.35
F4D_overlap      9.28  13.55
F_filt           7.38   7.26
F_filt_env       7.89   8.87
F_filt_env_conv  8.68   7.11
F_wind           5.36   5.36
```

## Two-state model

- Emission means: high **76.4 +/- 13.8 kt**, low **44.7 +/- 7.1 kt**
- Assigned 27,910 of 28,156; unassigned 246 (0.87%)
- Base rate **3.364%**
- pi_high = **2.32%** (0.69x base rate); outcome censored for 13.3% of this class
- pi_low = **4.55%** (1.35x base rate); outcome censored for 29.4% of this class
- P(high -> high) = 0.9572 [0.9539, 0.9603]
- P(high -> low) = 0.0428 [0.0397, 0.0461]
- P(low -> high) = 0.0532 [0.0497, 0.0568]
- P(low -> low) = 0.9468 [0.9432, 0.9503]
- cross = **0.0960** [0.0915, 0.1003]
- Median dwell (timestamps): high **96 h**, low **42 h**
- Consecutive record pairs exactly 6 h apart: 80.8% (transition matrix uses these only)
- Viterbi and forward-filtered classes agree on 94.98% of assigned observations
- Boundary-crossing frequency per 6-h pair: K=2 0.0485

## Intensity threshold

- Implied threshold ~**60 kt**
- Minority-class observations: **353** of 27,910 (**1.26%**)

## Indicator overlap

- n_test: 19198
- n_transition: 670
- n_transition_causal: 708
- n_threshold: 759
- pct_agree_transition_threshold: 99.54
- pct_agree_causal_threshold: 94.47
- n_threshold_only: 89
- n_threshold_only_RI: 0
- mean_future_dV24_threshold_only: -6.24
- n_transition_only: 0

## Case studies


```
  storm  year  storm_id  n_records  peak_kt  hours_to_peak  first_high_class_h  n_RI_records                             RI_hours                 RI_winds
 Haiyan  2013 1330_2013         29    125.0           84.0                30.0             6 [18.0, 24.0, 30.0, 36.0, 42.0, 48.0] [45, 55, 60, 65, 75, 85]
Surigae  2021 2102_2021         45    120.0           96.0                42.0             1                               [72.0]                     [90]
  Trami  2018 1824_2018         52    105.0           84.0                30.0             0                                   []                       []
```

## Conditional tests


```
                  flag                scheme  n_info  info_frac    or_mh  or_lo      or_hi  p_perm   rd_mh   rd_lo   rd_hi
       flag_membership                  none       1     1.0000   0.6263 0.5297     0.7405  0.0000 -0.0137 -0.0200 -0.0077
       flag_membership                    Vt       4     0.3415   3.2138 1.1554     8.9391  0.0880  0.0275  0.0131  0.0434
       flag_membership             Vt_x_dV12       9     0.1320  30.6456 3.2559   288.4446  0.0007  0.0645  0.0382  0.0733
       flag_membership      Vt_x_dV12_x_dV24      20     0.0675 138.4802 1.1204 17115.4621  0.0007  0.0737  0.0382  0.0756
       flag_membership Vt_x_dV12_x_shear_sst      32     0.0358  20.5252 2.2888   184.0609  0.0056  0.1083  0.0251  0.0673
       flag_transition                  none       1     1.0000   5.8848 4.6292     7.4809  0.0000  0.1086  0.0849  0.1337
       flag_transition                    Vt       6     0.4394   8.4293 5.7989    12.2530  0.0000  0.1190  0.0930  0.1468
       flag_transition             Vt_x_dV12      12     0.0733   2.2076 1.3701     3.5570  0.0018  0.0614  0.0276  0.0920
       flag_transition      Vt_x_dV12_x_dV24      37     0.0665   2.0961 1.2837     3.4228  0.0031  0.0606  0.0221  0.0895
       flag_transition Vt_x_dV12_x_shear_sst      54     0.0427   1.9579 1.1923     3.2152  0.0090  0.0817  0.0121  0.0890
flag_transition_causal                  none       1     1.0000   4.5673 3.5504     5.8754  0.0000  0.0838  0.0617  0.1060
flag_transition_causal                    Vt       6     0.4394   6.4455 4.5321     9.1666  0.0000  0.0921  0.0692  0.1149
flag_transition_causal             Vt_x_dV12      16     0.1240   1.5590 0.9541     2.5474  0.0758  0.0274 -0.0009  0.0550
flag_transition_causal      Vt_x_dV12_x_dV24      41     0.0804   1.2454 0.7302     2.1241  0.5021  0.0156 -0.0183  0.0444
flag_transition_causal Vt_x_dV12_x_shear_sst      58     0.0486   1.2505 0.7319     2.1367  0.4723  0.0260 -0.0196  0.0399
        flag_threshold                  none       1     1.0000   5.0768 4.0010     6.4419  0.0000  0.0928  0.0720  0.1153
        flag_threshold                    Vt       6     0.4394   7.1298 4.8830    10.4104  0.0000  0.1043  0.0801  0.1297
        flag_threshold             Vt_x_dV12      14     0.1050   1.5789 0.9680     2.5755  0.0701  0.0353 -0.0017  0.0683
        flag_threshold      Vt_x_dV12_x_dV24      37     0.0726   1.5762 0.9553     2.6009  0.0784  0.0376 -0.0023  0.0689
        flag_threshold Vt_x_dV12_x_shear_sst      49     0.0408   1.4934 0.8965     2.4878  0.1425  0.0491 -0.0116  0.0707
```

## Precursor

- RI onsets: **292**

```
 lag_h  high  low  missing  total  pct_high_of_valid
     6    50  153       89    292               24.6
    12    35  147      110    292               19.2
    18    24  125      143    292               16.1
    24    19  110      163    292               14.7
```

## Environmental separation


```
        var  D_class   D_RI
      sst_C   0.0466 0.3547
      shear   0.1034 0.1356
   so26chgt   0.0570 0.4163
mpi_gap_obs   0.9750 0.2544
         tp   0.1608 0.0813
       r700   0.0719 0.1251
      vo850   0.5127 0.1731
   sohtc300   0.1756 0.2527
```

## Supervised baselines


```
                           feature_set  n_features  auc_test  pr_auc_test  brier_test  base_rate_test  auc_cv_storm_mean  auc_cv_storm_sd
    Non-causal smoother\n+ environment           6    0.9532       0.5461      0.0222          0.0316             0.9671           0.0089
          Causal filter\n+ environment           6    0.8340       0.1080      0.0297          0.0316             0.8721           0.0218
          Raw quantised\n+ environment           6    0.8283       0.1084      0.0298          0.0316             0.8698           0.0232
       Raw + environment\n+ convective          12    0.8255       0.1165      0.0297          0.0316             0.8723           0.0238
Intensity +\nbackward $\Delta V_{24h}$           2    0.8408       0.1333      0.0290          0.0316             0.8239           0.0243
                Current intensity only           1    0.5419       0.0331      0.0306          0.0316             0.5823           0.0358
```
- PR-AUC ratio, non-causal to causal: **5.06**
- Correlation of smoother residual with forward 24-h change: **+0.550**; causal filter -0.376

## Epoch sensitivity


```
    epoch     n  storms  base_rate  pct_dV6_zero  mean_V  pct_high  pi_high  pi_low  cross  refit_mu_high  refit_mu_low
1977-1986  5597     260       3.76         56.63   59.09     44.17     3.52    4.01   0.10          75.86         44.97
1987-2005 12293     504       2.15         51.59   60.32     49.88     1.16    3.41   0.09          76.36         45.10
2006-2024 10266     456       4.63         50.34   59.90     46.86     3.20    6.16   0.09          77.59         42.78
```

## Higher-state structure


```
 K                          means                                diag                                                                                                                                                                  matrix  boundary_crossing_freq
 3             [82.1, 56.2, 40.3]               [0.941, 0.847, 0.891]                                                                                                        [[0.941, 0.059, 0.0], [0.08, 0.847, 0.073], [0.0, 0.109, 0.891]]                0.062477
 4       [85.7, 61.9, 44.9, 35.0]        [0.937, 0.844, 0.837, 0.647]                                                              [[0.937, 0.063, 0.0, 0.0], [0.072, 0.844, 0.084, 0.0], [0.0, 0.1, 0.837, 0.062], [0.0, 0.0, 0.353, 0.647]]                0.058404
 5 [88.6, 66.5, 49.4, 40.0, 35.0] [0.933, 0.839, 0.804, 0.567, 0.647] [[0.933, 0.067, 0.0, 0.0, 0.0], [0.069, 0.839, 0.089, 0.003, 0.0], [0.0, 0.105, 0.804, 0.073, 0.019], [0.0, 0.0, 0.303, 0.567, 0.129], [0.0, 0.0, 0.064, 0.289, 0.647]]                0.073306
```

## Supplementary diagnostics

- mpi_index_kt_min: 14.6697
- mpi_index_kt_max: 20.4293
- mpi_index_kt_mean: 18.8970
- mpi_index_kt_sd: 0.6371
- corr_mpi_gap_obs_with_V: -0.9995
- n_runs_stable: 147
- mean_max_pi_pct_stable: 4.8245
- mean_max_pi_pct_unstable: 7.0974
- max_pi_pct_stable_F_wind: 5.3603
- first_unstable_K_F_wind_diag: None
- first_unstable_K_F_wind_full: None
- max_pi_pct_stable_F4D_overlap: 4.4022
- first_unstable_K_F4D_overlap_diag: 2
- first_unstable_K_F4D_overlap_full: 3
- max_pi_pct_stable_F2D_nonoverlap: 6.0449
- first_unstable_K_F2D_nonoverlap_diag: 4
- first_unstable_K_F2D_nonoverlap_full: 6
- max_pi_pct_stable_F_filt: 7.3813
- first_unstable_K_F_filt_diag: None
- first_unstable_K_F_filt_full: 5
- max_pi_pct_stable_F_filt_env: 4.7212
- first_unstable_K_F_filt_env_diag: 4
- first_unstable_K_F_filt_env_full: 3
- max_pi_pct_stable_F_filt_env_conv: 8.5248
- first_unstable_K_F_filt_env_conv_diag: 6
- first_unstable_K_F_filt_env_conv_full: 4
- pct_configs_seed_sd_below_1pp: 96.8750
- median_seed_sd_pp: 0.0407
- high_share_pct_of_assigned: 48.0652
- lat_p10_high: 13.5000
- lat_p90_high: 31.1000
- lat_p10_low: 10.8000
- lat_p90_low: 33.1000