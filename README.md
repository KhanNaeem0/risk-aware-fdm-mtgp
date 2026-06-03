# Risk-Aware Multi-Objective Optimisation of FDM via MTGP-ICM

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/)

Reference implementation for the paper:

> **Risk-Aware Multi-Objective Optimisation of Fused Deposition Modelling via
> Multi-Task Gaussian Process Regression and Asymmetric Bayesian Loss Functions**
> Khan Naeem and Jianjun Wang.
> *Journal of Intelligent Manufacturing* (under review), 2026.

---

## Overview

This repository implements a **risk-aware multi-objective process-optimisation
framework** for fused deposition modelling (FDM). A **multi-task Gaussian process
with intrinsic coregionalisation (MTGP-ICM)** couples the four correlated
mechanical responses and shares statistical strength under limited data. Three
**closed-form asymmetric Bayes-risk estimators** (LINEX, precautionary, and
entropy losses) quantify the directional risk of unsafe over-prediction, and are
combined with an **EHVI–NSGA-II** Pareto search and a **four-method MCDM
consensus** to expose two deployment-context optima. Prediction intervals are
calibrated with a **split-conformal** layer and a **deployment knock-down factor
(KDF)**.

**Responses:** production time, elastic modulus, compressive strength,
strain-energy density.
**Inputs:** layer thickness, nozzle temperature, infill density, print speed.

---

## Repository contents

| File | Description |
|------|-------------|
| `naeem_LOCKED_real.ipynb` | Complete, self-contained pipeline (data, MTGP-ICM fit, LOO-CV, EHVI–NSGA-II Pareto search, closed-form Bayesian risk, MCDM consensus, confirmation, conformal + KDF calibration, simulation safety demonstration, and all publication figures). The 38-specimen dataset is embedded in the notebook. |
| `README.md` | This file |
| `requirements.txt` | Python dependencies |
| `LICENSE` | MIT License |

> The notebook is the single source of truth for every value reported in the
> manuscript. It runs end-to-end with a fixed random seed.

---

## Reproducing the results

```bash
git clone https://github.com/<your-username>/risk-aware-fdm-mtgp.git
cd risk-aware-fdm-mtgp
pip install -r requirements.txt
jupyter notebook main.ipynb
```

Then **Run All**. The pipeline is deterministic (primary seed `42`; the five-seed
set `{42, 123, 456, 789, 2024}` is used for hypervolume-stability estimates).
The final cell prints all manuscript numbers — leave-one-out R², the learned ICM
coregionalisation matrix, ARD importances, Pareto size and hypervolume, entropy
weights, the dual-pathway optima, confirmation metrics, and the knock-down
factor — and exports them to JSON.

**Built with:** NumPy, SciPy, scikit-learn, pandas, Matplotlib, PyTorch,
GPyTorch, and pymoo.

---

## Citation

If you use this code, please cite the paper and the archived release:

```bibtex
@article{NaeemWang2026FDM,
  title   = {Risk-Aware Multi-Objective Optimisation of Fused Deposition Modelling
             via Multi-Task Gaussian Process Regression and Asymmetric Bayesian
             Loss Functions},
  author  = {Naeem, Khan and Wang, Jianjun},
  journal = {Journal of Intelligent Manufacturing},
  year    = {2026},
  note    = {Under review}
}
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
