# MtbAIM

**Machine-learning prediction of activity and MIC-family endpoints against *Mycobacterium tuberculosis*.**

MtbAIM predicts compound activity against **drug-susceptible (DS)** and **drug-resistant (DR)** *M. tuberculosis* directly from SMILES.

The current deployment provides:

- DS activity classification
- DR activity classification
- DS MIC, MIC90, and MIC99 prediction
- DR MIC, MIC90, and MIC99 prediction

---

## Run in Google Colab

The easiest way to use MtbAIM is through the Google Colab notebook:

**Run MtbAIM prediction:**[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/jasdeep002/MtbAIM/blob/main/MtbAIM_predictor.ipynb)

Open the notebook in Google Colab and select:

**Runtime → Run all**

The notebook automatically downloads the deployment models from Hugging Face, performs integrity and feature-reproduction checks, and launches a Gradio prediction interface.

No local installation or permanent server is required.

---

## Input

Users can either:

- paste SMILES directly; or
- upload a CSV containing a SMILES column.

Recognized column names include:

```text
SMILES
smiles
canonical_smiles
standardized_smiles
```

A maximum of **100 compounds can be submitted per run**.

Example:

```text
CCO
CCN
c1ccccc1
CC(=O)O
```

---

## Output

For each compound, MtbAIM reports:

- DS probability of activity
- DS Active/Non-active prediction
- DR probability of activity
- DR Active/Non-active prediction
- DS MIC
- DS MIC90
- DS MIC99
- DR MIC
- DR MIC90
- DR MIC99
- nearest-training-set molecular similarity

MIC-family predictions are displayed in **µM**.

A downloadable CSV additionally contains pMIC values, nM concentrations, 80/90/95% residual intervals, canonical SMILES, and task-specific applicability information.

---



| Task | Model |
|---|---|
| DS classification | ExtraTreesClassifier |
| DR classification | HistGradientBoostingClassifier |
| DS MIC | ExtraTreesRegressor |
| DS MIC90 | LightGBM |
| DS MIC99 | XGBoost |
| DR MIC | ExtraTreesRegressor |
| DR MIC90 | ExtraTreesRegressor |
| DR MIC99 | ExtraTreesRegressor |

---

## Deployment validation

Before predictions are enabled, the Colab notebook automatically verifies:

- deployment file SHA256 hashes;
- all eight serialized models;
- the 2265-feature schema;
- frozen RDKit/Morgan feature reproduction;
- reference Step29 predictions;
- a 100-SMILES inference stress test.

Prediction is stopped if these checks fail.

---


## Repository structure

```text
MtbAIM/
├── README.md
├── MTB_AI_Predictor_Step31B_HuggingFace_Colab.ipynb
├── example_smiles.csv
└── LICENSE
```

Large deployment model files are hosted separately on Hugging Face.

---

## Important notes

The DS and DR models are independent models.

MIC, MIC90, and MIC99 are also modeled independently and should be interpreted as separate predictions.

Low similarity to the corresponding training set may indicate that a query compound lies outside well-represented chemical space and should therefore be interpreted with additional caution.

Multi-fragment SMILES are retained and flagged rather than silently modified.

---

## Intended use

MtbAIM is intended for:

- virtual screening;
- compound prioritization;
- antimicrobial drug-discovery research;
- retrospective analysis of chemical libraries;
- hypothesis generation prior to experimental testing.

**MtbAIM is a research tool and is not intended for clinical diagnosis or treatment decisions.**

---

## Citation

If you use MtbAIM, please cite the associated manuscript.

**Citation information will be added following manuscript/preprint release.**

---

## Contact

For questions regarding MtbAIM, model development, or collaborations, please contact the corresponding author of the associated study.
