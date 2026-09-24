# Covariance-aware asymmetric Bayes risk for reliability-based process selection: an additive manufacturing study

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.20520421.svg)](https://doi.org/10.5281/zenodo.20520421)

Reference implementation for the paper:

> **Covariance-aware asymmetric Bayes risk for reliability-based process selection: an additive manufacturing study**
> Khan Naeem and Jianjun Wang.
> *Reliability Engineering & System Safety* (under review), 2026.

---

## Overview

In safety-critical process selection, the mechanical responses that determine
load-bearing capacity are strongly correlated. Resolving the capacity margin
one response at a time understates its variance and overstates the reliability
of the component, and no point-accuracy metric reveals this shortfall.

This repository implements a decision-stage procedure that integrates three
established components:

- a **coregionalized multi-task Gaussian process (MTGP-ICM)** that returns the
  joint posterior covariance of the correlated responses;
- a **closed-form asymmetric Bayes action** (LINEX loss) on a scalar capacity
  margin, which carries the full posterior covariance into the safety decision
  (Proposition 1);
- two safeguards, namely a **conservative input-dependent variance inflation**
  with jackknife conformal calibration, and a **deployment knock-down factor
  (KDF)** that removes the residual optimistic bias.

The procedure is verified on a controlled simulator with known ground truth,
an analytical cantilever-beam benchmark, and fused deposition modeling (FDM)
of polylactic acid (PLA) with measured specimens.

**Responses (mechanical):** elastic modulus (*y*₁), compressive strength
(*y*₂), strain-energy density (*y*₃).
**Inputs:** layer thickness, nozzle temperature, infill density, print speed.

Key quantities:

- **Capacity margin:** *M* = **c**ᵀ**y**_mech, with the conservative
  LINEX-optimal action *δ*⋆_M = **c**ᵀ**μ** − (*a*_M/2) **c**ᵀ**Σc**
- **Understatement at the operating point:** a response-by-response (diagonal)
  treatment understates the margin standard deviation by 1.39×, so a nominal
  95 % bound covers about 88 % and a design targeting *β* = 2.0 achieves 1.44
- **Cross-response correlation:** empirical *r* ∈ [0.93, 0.97]; learned latent
  *ρ* ∈ [0.85, 0.94]

---

## Repository contents

| File | Description |
|------|-------------|
| `main.ipynb` | Complete pipeline: 38-specimen dataset, MTGP-ICM fit, leave-one-out cross-validation, variance inflation, closed-form asymmetric Bayes action on the coregionalized margin, operating-point selection, conformal calibration, knock-down factor, controlled simulation, cantilever-beam benchmark, sensitivity and negative-transfer studies, and the publication figures. |
| `results_locked.xlsx` | Locked workbook of the numerical results produced by the notebook. |
| `dataset_S1.csv` | The complete N = 38 process–response dataset (Supplementary Table S1). |
| `README.md` | This file. |
| `requirements.txt` | Python dependencies. |
| `LICENSE` | MIT License. |

The notebook runs end-to-end with a fixed random seed (primary: 42).

---

## Reproducing the results

```bash
git clone https://github.com/<your-username>/risk-aware-fdm-mtgp.git
cd risk-aware-fdm-mtgp
pip install -r requirements.txt
jupyter notebook main.ipynb
```

Archived snapshot (Zenodo): https://doi.org/10.5281/zenodo.20520421

---

## Citation

If you use this code or data, please cite:

```bibtex
@article{Naeem2026MABRGP,
  author  = {Naeem, Khan and Wang, Jianjun},
  title   = {Covariance-aware asymmetric Bayes risk for reliability-based
             process selection: an additive manufacturing study},
  journal = {Reliability Engineering \& System Safety},
  year    = {2026},
  note    = {Under review}
}
```

---

## Authors

- **Khan Naeem**, School of Economics and Management, Department of Management
  Science and Engineering, Nanjing University of Science and Technology, and
  Jiangsu Province Engineering Research Center of Quality Improvement for
  High-end Equipment, Nanjing, China.
- **Jianjun Wang** (corresponding author), School of Economics and Management,
  Department of Management Science and Engineering, Nanjing University of
  Science and Technology, and Jiangsu Province Engineering Research Center of
  Quality Improvement for High-end Equipment, Nanjing, China.
  ORCID: [0000-0003-0323-0365](https://orcid.org/0000-0003-0323-0365) ·
  jjwang@njust.edu.cn

---

## Acknowledgements

This work was partially supported by the National Natural Science Foundation of
China (Grant Nos. 72571142 and 72171118).

## License

Distributed under the MIT License. See [`LICENSE`](LICENSE) for details.
