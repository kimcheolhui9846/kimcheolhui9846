# Kim Cheolhui

**AI / Data Science · Computer Vision · Reproducible ML**

### [Portfolio Website](https://kimcheolhui.vercel.app)

I build ML projects around one question:

> Can this result be trusted, reproduced, and explained?

Software Convergence student at Hankyong National University, focused on AI,
Data Science, and Computer Vision.

---

## Focus

| Data | Modeling | Evaluation | Engineering |
|---|---|---|---|
| Leakage | PyTorch | Macro F1 | Config-driven runs |
| Duplication | CMT / ConvNeXt | Balanced Accuracy | CLI pipelines |
| Label quality | YOLOv8 segmentation | Holdout design | Tests / CI |
| Class imbalance | FashionSigLIP retrieval | Run variance | Reproducibility docs |

```text
Define -> Collect -> Audit -> Model -> Evaluate -> Validate -> Redesign
```

---

## Featured Projects

### [fruit-freshness-classification](https://github.com/kimcheolhui9846/fruit-freshness-classification)

**Reproducible PyTorch image-classification research pipeline**

| Topic | Summary |
|---|---|
| Problem | 14-class fresh / rotten fruit classification |
| Model | CMT, Stratified 3-Fold, Mixup, EMA, TTA, ensemble |
| Metrics | Top-1, Macro F1, Balanced Accuracy, per-class errors |
| Engineering | Modular `src/`, TOML configs, CLI train/eval, unittest, GitHub Actions |
| Key audit | `1,618 / 5,372` holdout rows duplicated a training row |
| Boundary | Internal holdout only; not an external benchmark or production claim |

**What matters here:** The project recorded a high internal holdout result, then audited the dataset and
documented why the number should be read carefully. It also measured run-to-run
variance and treated small metric gains against a noise floor instead of reading
single-run improvements at face value.

---

### [fashion-recommendation](https://github.com/kimcheolhui9846/fashion-recommendation)

**Fashion recommendation pipeline redesigned after data-quality analysis**

| Topic | Summary |
|---|---|
| Data | 23,203 crawled fashion images |
| First path | CMT / ConvNeXt classification experiments |
| Audit | pHash leakage check, duplicate-label visual diagnosis |
| Redesign | Classification abandoned; detection + embedding retrieval adopted |
| Pipeline | YOLOv8s-seg -> mask crop -> FashionSigLIP -> cosine retrieval |
| Evidence | Tier 1 detection accuracy `46.1% -> 98.6%` on holdout folder labels |
| Boundary | Manual mAP set is partly independent; recommendation scores are rank-based |

**What matters here:** The project did not force a classification solution after the data showed weak
category boundaries. It reframed the task into coarse garment detection plus
multimodal image-text retrieval, then evaluated post-processing and Korean query
handling separately.

---

## How I Work

`Question the metric` · `Audit the data` · `Control the experiment` ·
`Measure variance` · `Document limitations` · `Make it reproducible`

---

## Tech Stack

**Languages**

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)

**AI / ML**

![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)
![torchvision](https://img.shields.io/badge/torchvision-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)
![scikit--learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikitlearn&logoColor=white)
![Hugging Face](https://img.shields.io/badge/Hugging%20Face-FFD21E?style=flat-square)
![YOLOv8](https://img.shields.io/badge/YOLOv8-111111?style=flat-square)
![FashionSigLIP](https://img.shields.io/badge/FashionSigLIP-4B5563?style=flat-square)
![timm](https://img.shields.io/badge/timm-4B5563?style=flat-square)

**Data / Research**

![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat-square&logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=flat-square)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat-square&logo=jupyter&logoColor=white)
![pHash](https://img.shields.io/badge/pHash-leakage%20audit-4B5563?style=flat-square)

**Engineering**

![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)
![unittest](https://img.shields.io/badge/unittest-3776AB?style=flat-square)
![pytest](https://img.shields.io/badge/pytest-0A9EDC?style=flat-square&logo=pytest&logoColor=white)

---

## Current Direction

Building AI / Data Science projects where the output is not just a model score,
but a documented chain of evidence: data quality, evaluation validity,
experiment control, and reproducibility.
