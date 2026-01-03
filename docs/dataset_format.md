# Dataset Format Specification

This document describes the **expected dataset format** required by the SwinUNETR CT segmentation pipeline implemented in this repository.

The specification is designed to support **multi-class volumetric CT segmentation** and is configurable to different label spaces (3-class or 5-class tasks).

---

## Supported Data Modality

- **Imaging modality:** Computed Tomography (CT)
- **Data type:** 3D volumetric images
- **File format:** NIfTI (`.nii.gz`)
- **Orientation:** Any (handled during preprocessing)
- **Voxel spacing:** Arbitrary (resampled during preprocessing if enabled)

---

## Directory Structure

The dataset must be organized under a single root directory as follows:

### Naming Rules

- Image and label file names must **match exactly**
- Each image must have a corresponding segmentation label
- File extensions must be `.nii.gz`

---

## Label Encoding

Segmentation masks must use **integer-valued labels** representing class IDs.

### Example (3-class configuration)

| Label ID | Class      |
| -------- | ---------- |
| 0        | Background |
| 1        | Lung       |
| 2        | Heart      |
| 3        | Trachea    |

> The number of classes and their semantic meaning are controlled via the configuration file (e.g., `num_classes`, `class_names`).

---

## Image and Label Requirements

- Images and labels must be:
  - spatially aligned
  - in the same resolution before resampling
  - free of NaN or invalid values
- Labels must be **single-channel integer masks**
- No intensity normalization should be applied to labels

---

## Preprocessing Assumptions

The pipeline may apply the following preprocessing steps (configurable):

- HU intensity clipping
- Intensity normalization
- Spatial resampling to a target voxel spacing
- Cropping or patch-based sampling
- Data augmentation (training only)

These operations assume **consistent image–label alignment**.

---

## Configuration Interface

Dataset paths and properties are controlled through YAML configuration files:

```yaml
data:
  root: /path/to/data_root
  images_tr: imagesTr
  labels_tr: labelsTr
  images_val: imagesVal
  labels_val: labelsVal
  file_ext: ".nii.gz"

task:
  num_classes: 4
  class_names: ["background", "lung", "heart", "trachea"]
```
