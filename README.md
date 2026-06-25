# A covariance-aware asymmetric Bayes-risk method for safe process selection in additive manufacturing

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/)

Reference implementation for the paper:

> **A covariance-aware asymmetric Bayes-risk method for safe process selection in additive manufacturing**
> Khan Naeem and Jianjun Wang.
> *Reliability Engineering & System Safety* (under review), 2026.

---

## Overview

This repository implements a **reliability-based process-selection framework**
for fused deposition modelling (FDM) of load-bearing polymer parts. A
**multi-task Gaussian process with intrinsic coregionalisation (MTGP-ICM)**
models three correlated mechanical responses — elastic modulus, compressive
strength, and strain-energy density — jointly, sharing statistical strength
under a limited experimental budget (*N* = 38). A **closed-form asymmetric
Bayes-risk action** (LINEX loss) on a scalar capacity margin propagates the
learned cross-response covariance into the safety decision itself, yielding a
conservative operating point deployed under **split-conformal prediction
intervals** and a **deployment knock-down factor (KDF)**.

**Responses (mechanical):** elastic modulus (*y*₁), compressive strength
(*y*₂), strain-energy density (*y*₃).  
**Inputs:** layer thickness, nozzle temperature, infill density, print speed.

Key reliability quantities:
- **Capacity margin:** *M* = **c**ᵀ**y**ₘₑcₕ with conservative LINEX-optimal
  action *δ*⋆_M = **c**ᵀ**μ** − (*a*_M/2) **c**ᵀ**Σc**
- **Reliability index:** *β* ≈ 1.64 at nominal 95% coverage (full covariance)
  vs. *β* ≈ 1.09 under independent-output approximation
- **Cross-response correlation:** empirical *r* ∈ [0.93, 0.97]; learned latent
  *ρ* ∈ [0.79, 0.97]

---

## Repository contents

| File | Description |
|------|-------------|
| `main.ipynb` | Complete, self-contained pipeline: 38-specimen dataset, MTGP-ICM fit, leave-one-out cross-validation, closed-form Bayesian risk on coregionalised margin, direct conservative-margin operating-point selection, split-conformal calibration, knock-down factor estimation, controlled simulation, analytical cantilever-beam benchmark, and all publication figures. |
| `README.md` | This file |
| `requirements.txt` | Python dependencies |
| `LICENSE` | MIT License |

> The notebook is the single source of truth for every value reported in the
> manuscript. It runs end-to-end with a fixed random seed (primary: 42).

---

## Reproducing the results

```bash
git clone https://github.com/<your-username>/risk-aware-fdm-mtgp.git
cd risk-aware-fdm-mtgp
pip install -r requirements.txt
jupyter notebook main.ipynb
```

Archived snapshot (Zenodo): (https://doi.org/10.5281/zenodo.20520421) *(added on release)*

---

## Authors

- **Khan Naeem** — Department of Management Science and Engineering,
  Nanjing University of Science and Technology, Nanjing, China.
- **Jianjun Wang** (corresponding author) — Department of Management Science and
  Engineering, Nanjing University of Science and Technology, Nanjing, China.
  ORCID: [0000-0003-0323-0365](https://orcid.org/0000-0003-0323-0365) ·
  jjwang@njust.edu.cn

---

## Acknowledgements

This work was partially supported by the National Natural Science Foundation of
China (Grant Nos. 72571142 and 72171118).

## License

Distributed under the MIT License. See [`LICENSE`](LICENSE) for details.
