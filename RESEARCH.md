# 🔬 Research & Quantitative Work

Research internships, lab replications, domain tooling built for real workflows, and quantitative modelling. Numbers quoted here come from evaluation code and result files in the repos, not from memory.

[← back to profile](https://github.com/rayan-arya)

---

## South Florida Tree Detection
[![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat&logo=pytorch&logoColor=white)](#) [![DeepForest](https://img.shields.io/badge/DeepForest-2ea043?style=flat)](#) [![YOLO](https://img.shields.io/badge/Ultralytics_YOLO-111F68?style=flat)](#) [![GeoPandas](https://img.shields.io/badge/GeoPandas%20%2F%20rasterio-139C5A?style=flat)](#) [![Role](https://img.shields.io/badge/Sole%20author%20of%20the%20pipeline-1f6feb?style=flat)](#)

Research intern, **UM Frost Institute for Data Science & Computing**, Summer 2026.

Detecting and classifying individual trees in drone orthomosaics across two very different sites: the University of Miami's Coral Gables campus and wetland plots in Big Cypress National Preserve. A 20-stage pipeline covering label construction, spatial splitting, three detector families, evaluation design, and a set of experiments built to falsify my own results.

**The finding I'm proudest of is a negative one.** At Gables, the model looked mediocre against the botanical inventory. So I sampled 100 false positives and hand-checked every one in QGIS:

> Of 100 sampled false positives: **94 were real trees the inventory never recorded.** 3 were errors (2 tree shadows, 1 bush). 3 were unsure.

The ground truth was the problem, not the detector. Rather than quietly claiming credit for all 94 (which would have reported precision near 0.96), I split them into genuine inventory gaps and true localization failures and reported a corrected range of roughly 0.34 to 0.61, labelling the higher figure an upper bound that is wrong. The parallel analysis on missed trees showed only 5.4% were true blindness; 94.6% had a box on or near the tree that simply fell below the IoU threshold.

🌳 **Labels.** Each of 6,988 confirmed inventory points gets a box: a clean crown polygon's extent where one exists, otherwise a data-derived ~6.98 m median fallback, every box tagged with its provenance so the label set stays auditable.
🗺️ **Splits are spatial, not random.** Two ~45 ha areas of interest, so the model can't memorize a neighborhood.
📏 **A random-scatter floor.** At ~1.6 m stem spacing, a 1.5 m match radius lets *uniformly random points* score respectable recall. Every number is reported alongside how much it beats random, which is what turns a mediocre F1 into a demonstrated null.
🧠 **A detector written from scratch** (`s20`): a residual encoder and bilinear decoder with skip connections and a CenterNet-style single-channel heatmap head at quarter resolution, ~2M parameters, no torchvision backbone and no pretrained weights, trained with a locally implemented penalty-reduced focal loss. Benchmarked under the identical split and protocol as the library models.

| Detector (Gables, distance-matched at 5 m) | Precision | Recall | F1 |
|---|---|---|---|
| From-scratch CenterNet (`s20`) | 0.369 | 0.488 | **0.420** |
| DeepForest, fine-tuned | 0.674 | 0.498 | **0.573** |
| YOLO26s | 0.647 | 0.674 | **0.660** |

🔬 **Falsifying my own negative result.** Big Cypress came out at F1 ≈ 0.11, barely above the random floor. Instead of shrugging, I tested the two comfortable excuses. A georeferencing sweep over offset, rotation and flip peaked sharply and exactly at the current placement, and plot polygons were axis-aligned to 0.0000°. Re-scoring against DBH-filtered subsets showed recall flat at ~17% even for canopy-sized trees. Both excuses rejected in writing. The conclusion is about the site, not the model.

> Repo lives under the project lead's account; the entire `treedetect/` pipeline (7,428 lines across 21 stages, plus its documentation and every committed metric) is mine.

&nbsp;

## Neural Module Networks replication
[![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat&logo=pytorch&logoColor=white)](#) [![Repository](https://img.shields.io/badge/Repository-6e40c9?style=flat&logo=github&logoColor=white)](https://github.com/rayan-arya/ucla_summer_of_ai)

Summer research intern, **UCLA Visual Intelligence Lab**, 2024.

Reimplemented Andreas et al., *Deep Compositional Question Answering with Neural Module Networks*, in modern PyTorch under a graduate mentor. The original 2016 implementation was built on a since-abandoned framework, so the work was as much archaeology as engineering: read the paper, read code that no longer runs, and rebuild the attention and image-feature modules so the result is reproducible today.

🧩 Compositional VQA, where a question is parsed into a layout and a network is assembled per question from reusable modules.
📚 Includes the deep learning textbook and blog exercises I worked through that summer, which is where the PyTorch came from.

&nbsp;

## QuPath digital pathology extensions
[![Java](https://img.shields.io/badge/Java%2025-ED8B00?style=flat&logo=openjdk&logoColor=white)](#) [![Gradle](https://img.shields.io/badge/Gradle-02303A?style=flat&logo=gradle&logoColor=white)](#) [![AWS](https://img.shields.io/badge/S3%20%2F%20DynamoDB-232F3E?style=flat&logo=amazonwebservices&logoColor=white)](#) [![Repository](https://img.shields.io/badge/Repository-6e40c9?style=flat&logo=github&logoColor=white)](https://github.com/rayan-arya/qupath-annotation-tools)

Data science intern, **Intracellular Technologies**, Summer 2026.

Two Java extensions for QuPath, built for a real digital pathology workflow with real failure modes.

🔬 **Aperio XML export.** Pathologists annotate in QuPath, but the scanning partner works in ImageScope and drives a 100x oil acquisition from those regions. This exports annotations into ImageScope-compatible XML at level-0 coordinates. The interesting part is the pre-flight validation: if the reported pixel size says 0.274 µm/px instead of 0.137, the analyst is on the 20x pyramid level and every exported coordinate would be off by exactly 2x. Catching that in software costs nothing. Catching it after a wasted 100x scan run costs a day.
📐 The minimum-region warning derives its threshold from the partner's stated 0.5 mm stage-alignment tolerance and the live calibration, rather than hard-coding a pixel count.
☁️ **Provenance export.** Serializes the annotation hierarchy to GeoJSON, uploads it with nine provenance tags, and writes a lineage record to DynamoDB, so training-data lineage is captured at write time inside the tool instead of reconstructed later from filenames.
🔌 The storage layer sits behind an interface with three interchangeable backends (local filesystem, logging mock, AWS) selected at a single call site. The AWS implementation is stubbed pending Identity Center access, and the README says so rather than implying otherwise.

&nbsp;

## Options analytics
[![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)](#) [![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat&logo=numpy&logoColor=white)](#)

Quantitative analyst, **TAMID Group**, University of Miami.

Black-Scholes pricing and the full Greek set written out from the calculus rather than imported, plus an implied-volatility solver using Newton-Raphson with vega as the derivative, guarded against near-zero and NaN vega and clamped to a sane sigma range. Built over SPX chains joined to index closes.

&nbsp;

## Quant signal predictor
[![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)](#) [![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat&logo=scikitlearn&logoColor=white)](#) [![Repository](https://img.shields.io/badge/Repository-6e40c9?style=flat&logo=github&logoColor=white)](https://github.com/rayan-arya/quant-signal-predictor)

An intraday SPY signal study: data collection, feature engineering, target exploratory analysis, and model training, kept as four separate notebooks so each stage can be read on its own.

&nbsp;

## BetAI
[![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)](#) [![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat&logo=scikitlearn&logoColor=white)](#) [![Repository](https://img.shields.io/badge/Repository-6e40c9?style=flat&logo=github&logoColor=white)](https://github.com/rayan-arya/bet-ai)

Fair-odds models for NFL and NBA games, built on raw ESPN and Sleeper APIs rather than a tidy dataset.

📊 Rolling pre-game team features and home-minus-away differentials, trained with a **strictly chronological** train / calibrate / test split and explicit probability calibration, because a betting model that isn't calibrated is just a classifier with opinions.
🏥 An injury layer that maps Sleeper's player statuses into log-odds adjustments applied before converting back to American odds.
💰 A de-vig, expected-value and fractional-Kelly sizing chain on top, so the output is a bet size rather than a probability.
📉 Best test log-loss was 0.646 at 58% accuracy on roughly 50 held-out games. Those are wide error bars and none of it is compared against a closing line, which is the honest read: this is a working pipeline, not an edge.
