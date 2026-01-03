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
