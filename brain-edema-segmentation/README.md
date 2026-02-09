# Quantitative MRI-Based Analysis of Brain Edema Using Segmentation Masks

This project presents a quantitative image analysis pipeline for the study of brain edema from 3D magnetic resonance imaging (MRI) data. 
Using expert-curated segmentation masks, the workflow extracts edema volume, anatomical distribution, and geometric lesion descriptors: longest axis.

## Dataset Description

The analysis was performed using the Pretreat-MetsToBrain-Masks dataset (Ramakrishnan et al., 2024), a large open-access collection of brain metastasis MRI scans with expert-annotated segmentation masks.

This dataset was selected due to its inclusion of T2-FLAIR MRI sequences, allowing visualization of brain edema. In FLAIR images, edema appears as hyperintense regions, reflecting fluid accumulation within the brain parenchyma.
The suppression of cerebrospinal fluid (CSF) signal enhances contrast and facilitates accurate edema delineation.

Expert-generated segmentation masks are provided for multiple lesion components, including peritumoral edema, which was the focus of this project. 
A total of 200 patient cases were analyzed using the edema segmentation label to compute volumetric and geometric metrics.

## Image Preprocessing

MRI images and segmentation masks were provided in NIfTI format. Preprocessing was performed using NiBabel and scipy.ndimage and included:

- Spatial alignment and rescaling to ensure consistency across images

- Resolution matching between anatomical atlases and segmentation masks

- Correction for differences in image orientation and voxel dimensions

- Edema-associated voxels were extracted directly from the segmentation masks to generate binary lesion masks, which served as the foundation for all downstream quantitative analyses.

## Methodology Overview

The project implements a Python-based image analysis pipeline designed to operate on large-scale 3D MRI datasets.

Key steps include:

- Identification of edema voxels using expert segmentation masks

- Spatial connectivity analysis to detect individual edema regions

- Computation of lesion volume, lesion count, and regional distribution

- Anatomical localization using a brain atlas

- Parallelized processing across multiple CPU cores for efficiency

## Atlas-Based Regional Analysis

![Overlay of the anatomical atlas and the lesions](image/atlas_brain.png)

Edema regions were overlaid onto an anatomical brain atlas to associate lesions with specific brain regions, enabling regional quantification and spatial interpretation.

## Segmentation Visualization

![Axial slices with overlaid edema segmentation](image/edema_mask.png)

Axial MRI slices were visualized with overlaid edema masks to qualitatively assess segmentation accuracy and spatial extent across different brain levels.

## Geometric Feature Extraction: Longest Axis

![Visualization of the edema with its corresponding longest axis](image/longest_axis.png)

In addition to volumetric measurements, the pipeline computes the longest axis of each edema region, providing a geometric descriptor of lesion extent.

This metric was derived from 3D spatial coordinates of lesion voxels. To ensure computational efficiency, memory-aware sampling strategies were applied for large lesions before computing pairwise distances in physical space.

## Quantitative Results

![Analysis of edema volume distribution and affected regions](image/Result_edemas.png)


The extracted metrics enable statistical analysis of edema burden and spatial distribution across patients and brain regions. Volume distributions and region-specific involvement can be directly visualized and compared.

---------------------------------

# Data Usage and Disclaimer

All MRI images, segmentation masks, and clinical metadata belong to the original dataset providers. No raw imaging data or sensitive clinical information is redistributed in this repository.

This project presents a methodological and technical summary of the analysis performed, along with representative visualizations, to demonstrate the quantitative image analysis workflow and its outputs.


