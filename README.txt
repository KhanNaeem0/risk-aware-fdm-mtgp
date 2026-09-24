MABR-GP — complete reproduction package (executed, results locked)
Covariance-aware asymmetric Bayes risk for reliability-based process selection
JRESS-D-26-04906

MABR_GP_COMPLETE_EXECUTED.ipynb   61 cells, all 32 code cells executed top to
                                  bottom in one session, zero errors, 18 min.
                                  Every output below is embedded in the file.
figs/    16 figures, each as PDF (vector) + PNG + TIFF at 600 dpi
tables/  table05_noise_bound.csv          Table 5  (main)
         table06_kdf_corroboration.csv    Table 6  (main)
         table10_ablation.csv             Table 10 (main)
         tableS3_6_sample_size.csv        S3.6     (supplement)  [NEW]
         tableS6_negative_transfer.csv    S6       (supplement)  [NEW]
dataset_S1.csv                    38 specimens with production time tau
MABR_GP_results_locked.xlsx       11 password-protected sheets (MABRGP-2026)

WHAT IS NEW RELATIVE TO THE PREVIOUSLY RELEASED NOTEBOOK
  Fig 5   ARD + Sobol (was ARD only)          answers Reviewer 1, Comment 1.6
  Fig 6   margin posterior at i*              answers Reviewer 2, Comment 2.4
  Tables 5, 6, 10                             answer AE-2, AE-3, Concern 3.7
  S5.1    weight / a_M sensitivity            answers Comment 2.6
  Fig S2  posterior-predictive check          computed, no typed-in numbers
  Fig S3  sample-size study (S3.6)            RECONSTRUCTED - see caveat
  Fig S5  negative transfer (S6)              RECONSTRUCTED - see caveat
  q_t     conformal multipliers               were quoted but never computed
  Fig 4b  slope tests printed, fitted bands removed

CAVEAT ON THE TWO RECONSTRUCTED SUPPLEMENT STUDIES
  The scripts behind S3.6 and S6 were not in the released notebook, so these
  two cells were written from the description in the supplement. They reproduce
  the qualitative pattern but not the published digits:

    S3.6  LOO coverage at N=20    91.7 %   supplement says 93.3 %
          infill range           27.6-29.9 %   supplement says 28.2-29.8 %
          margin variation        8.5 %   supplement says 5.7 %
    S6    ICM vs independent   0.253/0.259 at rho3=0   supplement says 0.263/0.266
          rank-1 without kappa    0.791 (3.1x)   supplement says 0.689 (2.6x)
          rank S>=2 selected      44-52 %   supplement says 48-58 %

  Before submission, either (a) restore the authors' original scripts and keep
  the published numbers, or (b) adopt these recomputed values and update the
  supplement text accordingly. Do not ship both.

STILL MISSING (flagged in the verification report)
  - Friedman test and the four Table 2 baselines (SVR, stacking, SUR, indep GP)
  - Table 8 accuracy columns contradict the code (post-hoc widening cannot
    change R^2 or MAPE)
  - Section 3.1 says the noise term enters the likelihood; the code adds it to
    the predictive variance after fitting

Environment: python 3.11, torch 2.14, gpytorch 1.15.2, SEED = 0 throughout.
