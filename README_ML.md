# Gesture Instruction and Children's Eye Movements

Does seeing a teacher gesture change how children *look at* math problems later, when they solve them on their own? This project uses eye tracking, mixed-effects models, and machine learning to find out.

**Methods:** linear mixed-effects models · support vector machines · repeated resampling · permutation-style control models · R (`lme4`, `emmeans`, `caret`, `tidyverse`)

## 

## The question

Children often misread math equivalence problems like `3 + 6 + 5 = 3 + \_\_`, treating the equal sign as "put the answer here" instead of "both sides are equal." Instruction that includes gesture helps children learn these problems, but it's unclear *what* gesture changes. One possibility: gesture reorganizes how children visually take in a problem, and that change persists after instruction ends.

## 

## The study

* Children in grades 1–3 watched a short instructional video on equivalence problems, either with the teacher gesturing or speech only (same script, same body position).
* They then solved 16 problems on their own while wearing a head-mounted eye tracker.
* Gaze was coded into five areas of interest (AOIs): the three addends on the left (A, B, C) and the two positions on the right side of the equal sign (D, E).
* Final eye-tracking sample: 58 children - 51 Eye-tracking with good tracks. 
## 

## Approach

1. **Fixation counts:** mixed-effects models comparing how often children in each condition looked at each AOI.
2. **Gaze transitions:** mixed-effects models of how children moved their eyes *between* AOIs (25 possible transitions, e.g., A → B).
3. **Classification:** radial-kernel SVMs trained to predict instruction condition from transition counts alone. Each model was trained 64 times on balanced 80/20 splits, so chance accuracy is 50%.
4. **Control model:** the same models trained to predict a *random* A/B grouping of children. Because each child contributes many problems, a model could do well just by recognizing individual children. The control shows how much accuracy that alone produces.
5. **Ablation:** retraining without transitions involving the first addend (A), to test whether that one difference drives the result.

## 

## Key findings

* **Children taught with gesture looked at the first addend more** (t(88.8) = 2.42, p = .018), with no differences at other AOIs.
* **Their gaze moved differently:** more A → A and A → B transitions, more refixations on C and E, and fewer C → B transitions.
* **Gaze patterns predicted instruction condition:** transition counts alone classified condition with **60.1%** test accuracy.
* **That's above the participant-recognition baseline:** the random A/B control reached 56.1%, and the condition model was significantly more accurate (t(120.2) = 5.79, p < .001).
* **The first addend explains part of the effect, not all of it:** without A transitions, accuracy dropped to 57.3%, still above the control.

## 

## Limitations

* Train/test splits were made at the problem level, so the same child can appear in both. The random-label control estimates how much this inflates accuracy, but a participant-level split would be stronger. The sample was too small for one here. To address this, we ran comparable controls with randomly assigned conditions. This randomized approach was less accurate than our models which predicted instruction. 



* Data collection ended early because of the COVID-19 pandemic, and the analyses were exploratory. A preregistered replication with a modern eye tracker is the natural next step.
* In this sample, the two conditions did not differ in posttest accuracy, so these gaze differences show that gesture changes *how* children approach problems, not that it improved their scores here.

## 

## Repository contents

|File|What it does|
|-|-|
|[`analysis/01\_classification\_models.Rmd`](analysis/01_classification_models.Rmd)|Builds transition features, balances groups, and trains the SVM, control, and ablation models (64 repetitions each)|
|[`analysis/02\_paper\_analyses.Rmd`](analysis/02_paper_analyses.Rmd)|Fixation-count and transition models, model-performance comparisons, and paper figures|

Each `.Rmd` has a knitted `.md` version that GitHub displays with output and figures.

## 

## Data

Participant data are not included because they come from child participants and are covered by IRB protections. The notebooks document every processing step.

## 

## About

Part of my dissertation research in the Communication, Cognition, and Learning Lab at the University of Iowa (advisor: Susan Wagner Cook). Manuscript in preparation.

