# Summer Research Project: Automated Kidney Stone Location Identifier
### Resource Guide

---

## Project Background

We can currently identify and measure kidney stones in CT images using an AI pipeline that:
1. Segments the kidney using deep learning,
2. Uses computer vision to locate the stone via its centroid, and
3. Classifies its placement using superior/inferior and left/right spatial grids.

This summer, **six expert reviewers** will view CT-identified stones and label each one as **Upper, Mid, Renal Pelvis, or Lower**. Using these expert labels as ground truth, we will help develop machine learning and visual tools that can **automatically assign stone location** — reducing the need for manual review.

## Goals for the Summer

1. Submit a poster abstract to the **Mid-Atlantic Bioinformatics Conference (MABC)**.
2. Learn the basics of machine learning.
3. Learn how stone location impacts clinical outcomes.

## After the Summer (Stretch Goal)

- Possibly expand the work into a manuscript and submit an abstract/paper to a journal.

---

## Research to Start Now

### 1. How Stone Location Impacts Clinical Outcomes

Goal: build an annotated bibliography (aim for 15-20 citations) covering both **stone passage vs. surgery** and **obstruction**.

**Stone passage vs. surgery / location as a predictor:**
- Coll DM, Varanelli MJ, Smith RC. *Relationship of spontaneous passage of ureteral calculi to stone size and location as revealed by unenhanced helical CT.* AJR 2002 — the classic paper establishing that both size and ureteral location (proximal/mid/distal/UVJ) predict spontaneous passage rate. [AJR link](https://ajronline.org/doi/10.2214/ajr.178.1.1780101) | [PubMed](https://pubmed.ncbi.nlm.nih.gov/11756098/)
- "Size matters: the width and location of a ureteral stone accurately predict the chance of spontaneous passage" (2017) — builds a prediction model from stone width + location. [Free full text (PMC)](https://pmc.ncbi.nlm.nih.gov/articles/PMC5635101/)
- Sfoungaristos S, Kavouras A, Perimenis P. *Predictors for spontaneous stone passage in patients with renal colic secondary to ureteral calculi.* Int Urol Nephrol 2012 — location (upper/mid/lower ureter) plus inflammatory markers as predictors. [Springer link](https://link.springer.com/article/10.1007/s11255-011-9971-4)
- AUA Surgical Management of Kidney and Ureteral Stones Guideline (2025) — current evidence-based framework for when watchful waiting / medical therapy vs. surgical intervention is recommended. [AUA Guideline](https://www.auanet.org/guidelines-and-quality/guidelines/surgical-management-of-kidney-and-ureteral-stones)
- Lower pole stones specifically are a harder case for treatment planning — the "Lower Pole I" trial compared SWL vs. PCNL outcomes by location. Good review: [Treatment of renal lower pole stones: an update](https://www.scielo.br/j/ibju/a/VncGbsBsbJmZNh4NBGqXtTv/?lang=en)
- Upper vs. lower pole access considerations for surgery: [AUA News — Upper vs Lower Pole Percutaneous Renal Access](https://auanews.net/issues/articles/2024/june-extra-2024/upper-vs-lower-pole-percutaneous-renal-access)

**Stone obstruction / hydronephrosis:**
- Hydronephrosis is commonly graded with the **Society for Fetal Urology (SFU) 0-4 scale** based on renal pelvis/calyceal dilation — a good starting framework for understanding obstruction severity. [Overview (Biology Insights)](https://biologyinsights.com/hydronephrosis-grading-clarifying-classifications/) | [Wikipedia overview](https://en.wikipedia.org/wiki/Hydronephrosis)
- "Association Between Nephrolith Size and Location and Grade of Hydronephrosis" — directly relevant to this project's question of how location relates to obstruction severity. [Free full text (PMC)](https://pmc.ncbi.nlm.nih.gov/articles/PMC11857376/)
- "Association between grades of Hydronephrosis and detection of urinary stones by ultrasound imaging" — stone detection rates across hydronephrosis grades. [Free full text (PMC)](https://pmc.ncbi.nlm.nih.gov/articles/PMC6115544/)


### 2. Example Posters and Abstracts

- [Mid-Atlantic Bioinformatics Conference (MABC) site](https://www.midatlanticbioinformatics.org/) — check the agenda/past programs for example abstract topics and formatting expectations.
- Colin Purrington's **Designing Conference Posters** guide — the standard reference for academic poster layout, font sizes, and section structure (with free PowerPoint templates). [Guide](https://colinpurrington.com/tips/poster-design/)
- **Better Posters** blog by Zen Faulkes — more modern, minimalist poster design philosophy ("one big message" posters). Worth comparing against the Purrington style. Search "betterposters.blogspot.com."
- University research-guide pages collecting real student poster examples are also useful for seeing finished products (search "[university name] undergraduate research poster examples").

### 3. Data Types for Data Science

- Google's **Machine Learning Crash Course** has dedicated, free modules on this exact topic:
  - [Working with numerical data](https://developers.google.com/machine-learning/crash-course/numerical-data)
  - [Working with categorical data](https://developers.google.com/machine-learning/crash-course/categorical-data)
  **categorical/nominal** (unordered categories, e.g. stone location), and **numeric** (continuous measurements, e.g. stone size in mm) features.
- **Target variable for this project:** stone location (Upper / Mid / Renal Pelvis / Lower) is a **multi-class categorical target**. 

### 4. Machine Learning Algorithms

Recommended order: logistic regression → decision tree → random forest (each builds conceptually on the last).

- **StatQuest with Josh Starmer** (YouTube) — far and away the most approachable explanations of these algorithms, with no math background assumed. Look up "StatQuest: Logistic Regression," "StatQuest: Decision and Classification Trees," and "StatQuest: Random Forests Part 1" specifically. [Channel](https://www.youtube.com/@statquest) | [Full video index](https://statquest.org/video_index.html)
- **scikit-learn documentation** (the Python library you'll actually use to build these models):
  - [Logistic Regression](https://scikit-learn.org/stable/modules/linear_model.html#logistic-regression)
  - [Decision Trees](https://scikit-learn.org/stable/modules/tree.html)
  - [Random Forests (Ensemble methods)](https://scikit-learn.org/stable/modules/ensemble.html#forests-of-randomized-trees)


### 5. Machine Learning Evaluation Measures

- scikit-learn's **Model Evaluation** documentation covers all four measures listed below in one place, with multi-class examples: [Metrics and scoring](https://scikit-learn.org/stable/modules/model_evaluation.html)
- **StatQuest** again has short, clear videos worth watching alongside the docs: "StatQuest: Machine Learning Fundamentals: The Confusion Matrix," "ROC and AUC, Clearly Explained!"

  - **Accuracy** — % of predictions that were correct overall. Can be misleading if classes are imbalanced (e.g., if "Mid" stones are rare).
  - **Confusion Matrix** — a table showing predicted vs. actual class for every stone; the foundation all other metrics are built from. Essential for a 4-class problem like this one, since it shows *which* locations get confused with each other.
  - **F1 Score** — balances precision (how many predicted "Upper" stones really were Upper) and recall (how many actual "Upper" stones were caught); more informative than accuracy when classes are imbalanced.
  - **AUC** (Area Under the ROC Curve) — measures how well the model ranks/separates classes across all decision thresholds; for multi-class problems this is typically computed per-class (one-vs-rest) and averaged.

---
