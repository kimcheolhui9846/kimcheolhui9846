# Kim Cheolhui

**AI / Data Science | Computer Vision | Reproducible ML**

I build machine-learning projects by asking whether the data, split, metric, and
experiment design are trustworthy enough to support the result.

My current work is centered on computer vision and data science: dataset quality
audits, leakage checks, model evaluation, experiment control, failure analysis,
and reproducible PyTorch pipelines.

---

## About

I am Kim Cheolhui, a Software Convergence student at Hankyong National
University, working on AI and data science projects with a focus on computer
vision.

What interests me most is not only whether a model gets a high score, but why
that score appears, whether the evaluation is independent, and what limitations
should be documented before the result is trusted.

---

## Research / Engineering Focus

| Area | What I pay attention to |
|---|---|
| Data quality | duplication, leakage, label quality, class imbalance, dataset provenance |
| Modeling | CNN / Transformer vision models, PyTorch training, detection, segmentation, multimodal embeddings |
| Evaluation | Macro F1, balanced accuracy, holdout design, independent evaluation, per-class failure analysis |
| Experiment design | controlled comparisons, run-to-run variance, deterministic training, noise floor, reproducibility boundaries |
| Pipeline design | notebook-to-module refactoring, config-driven runs, CLI workflows, tests, CI |

```text
Problem Definition
  -> Data Collection
  -> Data Quality Audit
  -> Modeling
  -> Evaluation
  -> Result Validation
  -> Failure Analysis
  -> Experiment Redesign
  -> Reproducibility
```

---

## Featured Research Projects

### [fruit-freshness-classification](https://github.com/kimcheolhui9846/fruit-freshness-classification)

A reproducible PyTorch research pipeline for fresh/rotten fruit image
classification.

| | |
|---|---|
| Problem | 14-class fresh / rotten fruit classification from the `Densu341/Fresh-rotten-fruit` dataset |
| Approach | CMT classifier, Stratified 3-Fold training, Mixup, configurable CE/Focal loss, EMA checkpoints, horizontal-flip TTA, raw-logit ensemble evaluation |
| Evaluation | Internal 5,372-image holdout with Top-1, Macro F1, Balanced Accuracy, top-k recovery, per-class metrics, and confusion analysis |
| Engineering | `src/` modular pipeline, shared TOML experiment config, training/evaluation CLIs, repository contract tests, Windows/Ubuntu GitHub Actions CI |

**Main research point:** the project does not treat a high holdout score as the
end of the story.

The frozen internal holdout result recorded Top-1 `0.9555`, Macro F1 `0.9037`,
and Balanced Accuracy `0.9000`. Afterward, a byte-level SHA-256 duplication
audit found that `1,618 / 5,372` holdout rows duplicated a training row. On rows
without such a duplicate, Top-1 was `0.9414`.

Instead of rewriting the result after seeing the issue, the repository keeps the
original metric as measured and documents the contamination effect, the
publication boundary, and why this is not an external benchmark or production
claim.

The later post-holdout research also measured run-to-run variance: three
identical baseline runs produced Macro F1 `0.901167`, `0.912041`, and
`0.901858`, giving a two-sigma noise floor of about `0.0122`. That changed how
small experimental gains were interpreted and led to a strict determinism check
with explicit seeding.

**What this shows:** data leakage analysis, honest metric interpretation,
experiment governance, deterministic training work, and reproducible ML
engineering.

---

### [fashion-recommendation](https://github.com/kimcheolhui9846/fashion-recommendation)

A fashion recommendation AI pipeline that was redesigned after the original
classification approach exposed data and label problems.

```text
Web-crawled fashion images
  -> noise filtering
  -> CMT / ConvNeXt classification experiments
  -> unexpectedly high validation accuracy
  -> pHash leakage check and duplicate-label diagnosis
  -> classification approach abandoned
  -> YOLOv8 segmentation + FashionSigLIP retrieval pipeline
```

| | |
|---|---|
| Data | 23,203 crawled fashion images across 22 original folders, later merged into coarser category systems |
| Initial finding | ConvNeXt validation accuracy reached 88.23%, then pHash and visual audits showed why the number needed scrutiny |
| Redesign | Detection handles coarse garment localization; FashionSigLIP embeddings handle image-text retrieval and finer style matching |
| Current pipeline | user image -> YOLOv8s-seg -> mask crop -> FashionSigLIP image embedding -> text embedding -> cosine similarity retrieval |
| Evaluation work | holdout Tier 1 accuracy, recommendation P@5 policy comparison, manual test set for box/mask mAP, Korean-query evaluation |

**Main research point:** the important result was not simply improving a model,
but changing the problem definition after the data contradicted the first
approach.

The project started with crawled data, noise removal, and classification
experiments. After high validation accuracy appeared, the repository documents a
pHash-based leakage check and visual duplicate-label diagnosis. The
classification path was then removed from the final system, and the pipeline was
reframed as detection plus multimodal retrieval.

For detection, the project used pretrained YOLOv8s-seg to generate boxes and
folder labels to assign the project categories. This was tested rather than
assumed: the pretrained model often found garment locations but gave unreliable
category names. Fine-tuning changed Tier 1 holdout accuracy from `46.1%` to
`98.6%`, while the documentation also notes that the manual mAP set is only
partly independent because its boxes originated from auto-labels accepted by a
human reviewer.

The recommendation side is evaluated as a retrieval system, not as a classifier.
One example: deduplicating detections by `confidence * area` improved P@5 from
`75.5%` to `87.3%` by preventing fragmented boxes from dominating the top
results. Korean text handling was also measured directly: domain dictionary
conversion performed better than a generic translation model for fashion loan
words.

**What this shows:** data collection, class imbalance analysis, leakage checks,
problem reformulation, segmentation, embedding retrieval, evaluation design, and
pipeline-oriented engineering.

---

## How I Work

- Question the metric before using it as evidence.
- Audit the dataset before trusting the split.
- Separate model performance from data leakage and evaluation artifacts.
- Prefer controlled comparisons over isolated scores.
- Measure variance when a claimed improvement is small.
- Document limitations instead of hiding them.
- Refactor notebooks into reusable, testable research pipelines when the work
  grows beyond exploration.

---

## Tech Stack

**Languages:** Python

**AI / ML:** PyTorch, torchvision, timm, Hugging Face datasets / hub,
Ultralytics YOLO, FashionSigLIP / open_clip, scikit-learn

**Data / Analysis:** NumPy, Matplotlib, Jupyter, image hashing, metric reports,
confusion analysis

**Engineering:** Git, GitHub Actions, CLI scripts, config-driven experiments,
`unittest`, `pytest`

---

## Current Direction

I am continuing to build AI / Data Science projects where the core question is:

> Can this result be trusted, reproduced, and explained?

Korean: 모델의 점수보다 데이터와 평가가 믿을 만한지 먼저 확인하는 AI / Data Science
개발자를 지향합니다.
