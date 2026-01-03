# SwinUNETR-CT-segmentation-adaptation

This repository presents a **reproducible end-to-end CT multi-class segmentation pipeline** based on **SwinUNETR**, a transformer-based U-Net architecture.

The original task provided for evaluation involved a **5-class CT segmentation problem**.  However, since the original dataset is not publicly available, this work validates the pipeline using a **public CT dataset with a different label space**, while preserving the original modeling, preprocessing, and training principles.

The focus of this adaptation is **pipeline understanding, correctness, and generalization**, rather than reproducing the exact original dataset.

The purpose of this work is to demonstrate the ability to:
1. Understand and refactor an existing medical image segmentation pipeline,
2. Adapt it to a new CT dataset with a different class configuration,
3. Execute training, inference, and evaluation in a clean, well-documented, and reproducible manner.

---

## Key Features

- **End-to-end pipeline:** dataset preparation → training → inference → evaluation  
- **Configurable label space:** adapted from an original **5-class** setup to a **3-class** segmentation task via configuration  
- **Reproducibility-focused design:** standardized scripts, configuration files, and result organization  
- **CT-aware preprocessing:** support for HU-based intensity normalization and spatial resampling  

---

## Dataset

Experiments are conducted using the public dataset:

**Chest CT Segmentation (lung, heart, trachea)**  
https://www.kaggle.com/datasets/polomarco/chest-ct-segmentation

This dataset provides volumetric CT scans with voxel-wise annotations for three anatomical structures.

### Label Definition

The current configuration uses **three foreground classes**, in addition to background:

| ID | Class       |
|----|-------------|
| 0  | Background  |
| 1  | Lung        |
| 2  | Heart       |
| 3  | Trachea     |

> **Note:** Some segmentation frameworks include background as an explicit class, while others treat it implicitly.  
> In this repository, the value of `num_classes` is configured to match the model output channels defined in the training configuration.

---

## Original Workflow and Adaptation

The original codebase provided for evaluation was primarily implemented as a sequence of Jupyter notebooks and designed for a **5-class CT segmentation task**.

This adaptation focuses on:
- Generalizing the pipeline to support **arbitrary numbers of segmentation classes** via configuration,
- Ensuring data loading and preprocessing steps remain robust when applied to a different CT dataset,
- Refactoring the workflow into reusable scripts suitable for reproducible experimentation.

The same pipeline can be reconfigured back to a **5-class segmentation setting** by modifying:
- `num_classes`
- `class_names`
- label mappings (if required)

---

## Repository structure

The repository is organized to separate configuration, execution logic, and results, following common best practices in machine learning research:

```bash
swinunetr-ct-seg-adaptation/
├── README.md
├── LICENSE
├── CITATION.cff
├── requirements.txt
├── .gitignore
├── configs/
│   └── chestct_3class.yaml
├── scripts/
│   ├── prepare_dataset.py
│   ├── train.py
│   ├── infer.py
│   ├── evaluate.py
│   └── visualize_predictions.py
├── src/
│   ├── data/
│   ├── models/
│   ├── losses/
│   └── utils/
├── notebooks/                # original and exploratory notebooks
├── runs/                     # experiment logs and checkpoints
├── results/
│   ├── metrics.json
│   ├── curves.png
│   └── qualitative/
├── docs/
│   └── dataset_format.md
└── data/
    └── README.md

```

