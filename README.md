<h1>
  [arXiv'25]  <img src="assets/morel.png" width="30" align="absmiddle">
  MoRel: Long-Range Flicker-Free 4D Motion Modeling via Anchor Relay-based Bidirectional Blending with Hierarchical Densification
</h1>

**<a href="mailto:s.kwak@etri.re.kr">Sangwoon Kwak</a>**<sup>1*</sup>, 
**<a href="mailto:weeyoungkwon@cau.ac.kr">Weeyoung Kwon</a>**<sup>2*</sup>, 
**<a href="mailto:jyj0120@etri.re.kr">Jun Young Jeong</a>**<sup>1</sup>, 
**<a href="mailto:joelkimgh@cau.ac.kr">Geonho Kim</a>**<sup>2</sup>,  
**<a href="mailto:wscheong@etri.re.kr">Won-Sik Cheong</a>**<sup>1</sup>, 
**<a href="mailto:jihyongoh@cau.ac.kr">Jihyong Oh</a>**<sup>2†</sup>  
<br>

<sup>1</sup>Electronics and Telecommunications Research Institute (ETRI)  
<sup>2</sup>Chung-Ang University  
<br>
*Equal contribution, †Corresponding author
<br>
<!-- * Official project page:  https://cmlab-korea.github.io/MoRel/
* Paper (arXiv):  -
* Code will be updated soon -->

[![Project Page](https://img.shields.io/badge/Project-Page-1E90FF)](https://cmlab-korea.github.io/MoRel/)
[![arXiv](https://img.shields.io/badge/arXiv-TBD-B31B1B.svg)](#)
![Stars](https://img.shields.io/github/stars/CMLab-Korea/MoRel?style=social)

This repository is the official PyTorch implementation of  
**“MoRel: Long-Range Flicker-Free 4D Motion Modeling via Anchor Relay-based Bidirectional Blending with Hierarchical Densification.”**

![teaser](./assets/teaser.png)  
Figure 1. MoRel enables long-range, flicker-free 4D reconstruction with temporally coherent details, even under large motions and topology changes.

## News
* Repository created and initial codebase is being organized.
* Paper under review; details will be updated after the review process.

## Code Release Plan
- [ ] Core MoRel training and rendering pipeline
- [ ] Anchor Relay-based Bidirectional Blending (ARBB) modules
- [ ] Hierarchical Densification utilities and analysis tools
- [ ] Dataset preparation and evaluation scripts

## Abstract

Recent advances in 4D Gaussian Splatting (4DGS) have extended the high-speed rendering capability of 3D Gaussian Splatting (3DGS) into the temporal domain, enabling real-time rendering of dynamic scenes. However, one of the major remaining challenges lies in modeling long-range motion-contained dynamic videos, where a naïve extension of existing methods leads to severe memory explosion, temporal flickering, and failure to handle appearing or disappearing occlusions over time.

To address these challenges, we propose a novel 4DGS framework characterized by an **Anchor Relay-based Bidirectional Blending (ARBB)** mechanism, named **MoRel**, which enables temporally consistent and memory-efficient modeling of long-range dynamic scenes. Our method progressively constructs locally canonical anchor spaces at key-frame time indices and models inter-frame deformations at the anchor level, enhancing temporal coherence.

By learning bidirectional deformations between key-frame anchors (KfA) and adaptively blending them through learnable opacity control, our approach mitigates temporal discontinuities and flickering artifacts. We further introduce a **Feature-variance-guided Hierarchical Densification (FHD)** scheme that effectively densifies KfAs while preserving rendering efficiency, based on an assigned level of feature variance.

To effectively evaluate our model's capability to handle real-world long-range 4D motion, we newly compose a long-range 4D motion-contained dataset, called **SelfCap<sub>LR</sub>**. It exhibits larger average dynamic motion magnitude and is captured in spatially wider environments compared to previous dynamic video datasets.

Overall, **MoRel** achieves temporally coherent and flicker-free long-range 4D reconstruction while maintaining bounded memory usage, demonstrating both scalability and efficiency in dynamic Gaussian-based representations.


## Method Overview
MoRel: An anchor-based 4D motion modeling framework for long-range, flicker-free 4D Gaussian Splatting.

![framework](./assets/figure_method_1.png)

### Global Canonical Anchor (GCA)
MoRel first trains a single **Global Canonical Anchor (GCA)** over the entire sequence from an initial point cloud.  
The GCA provides a **globally consistent** appearance prior and anchor features whose variances are later used to assign frequency-aware levels for FHD.

### Key-frame Anchors & Anchor Relay
Periodically placed **Key-frame Anchors (KfAs)** are initialized from the level-assigned GCA and locally refined around their key-frame indices.  
Each KfA acts as a **local canonical space** for its temporal neighborhood, forming an anchor relay that supports long-range modeling and random temporal access under bounded memory.

### Bidirectional Deformation & Blending
In the **Progressive Windowed Deformation (PWD)** stage, each KfA learns forward and backward deformation fields within a **local bidirectional deformation window**, with anchors loaded on demand to keep GPU memory bounded.  
The **Intermediate Frame Blending (IFB)** stage then learns temporal opacity weights to fuse neighboring KfAs, yielding **smooth transitions and consistent long-range motion**.

### Feature-variance-guided Hierarchical Densification
**Feature-variance-guided Hierarchical Densification (FHD)** uses the variance of anchor features as a proxy for local frequency, assigning levels and modulating gradient-based densification accordingly.  
Low-frequency structure is stabilized early, while high-frequency regions are refined later, improving reconstruction quality without exceeding the memory budget.


## Prepare Dataset
TBD;  

## Environment Setting
TBD;  


## Get Started
TBD;  

## Results
Please visit our [project page](https://cmlab-korea.github.io/MoRel/) for video demos, qualitative comparisons, and quantitative results.
