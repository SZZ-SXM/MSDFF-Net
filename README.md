# MSDFF-Net

> [Arbitrary-Direction SAR Ship Detection Method for Multi-Level Imbalanced Problems](Under reviewing)

<!-- [ALGORITHM] -->

## Abstract

Arbitrary-oriented ship detection in SAR imagery facilitates more precise and comprehensive target feature extraction across diverse scenarios. However, achieving optimal detection performance remains challenging due to multi-level imbalances, including object scale imbalance, feature utilization imbalance, and regression loss imbalance. In response to these challenges, this paper presents a Multi-Scale Dynamic Feature Fusion Network (MSDFF-Net), specifically developed for arbitrary-oriented SAR ship detection. First, to lessen impact of scale imbalance impact, a Multi-Scale Large-Kernel Convolution Block (MSLK-Block) is designed, integrating large-kernel with partitioned heterogeneous convolution to enhance the backbone network’s capacity for robust multi-scale feature representation. Second, a Dynamic Feature Fusion Block (DFF-Block) is introduced to optimize spatial and channel-level feature utilization, balancing the contributions of features across different dimensions. Third, to tackle regression loss imbalance, the Gaussian probability distributions (GPD) loss function is designed to account for the elliptical geometry of ship targets. Ablation studies confirm the contribution and efficacy of each component utilized in proposed methodology. Experimental evaluations on the R-SSDD, R-HRSID, and CEMEE datasets demonstrate that MSDFF- reaches top-tier performance standards, outperforming 21 existing deep learning-based SAR ship detectors. Specifically, MSDFF-Net achieves 93.95% precision, 94.72% recall, 91.55% mAP, 94.33% F1-Score, and 135.79 FPS on the R-SSDD dataset, with a parameter size of only 8.94 M. Finally, testing on two large-scale SAR images at different resolutions highlights MSDFF-Net’s strong transferability and deployment capability in real-world maritime scenarios.

<div align=center>
<img src="https://github.com/SZZ-SXM/MSDFF-Net/blob/main/data/1.png">
</div>

## Overall Structure

Our works are focused on the following three aspects: 
1) To mitigate the impact of scale imbalance in feature extraction, a multi-scale large kernel convolution block was introduced into backbone structure, leading to our proposal of a new backbone framework named MSLK-Net. MSLK-Net can more effectively extract multi-scale ship target features and both local and global information from the complex scene.
2) To enhance the model's perception ability in complex scenes and address the unbalanced utilization of spatial and channel features during the feature fusion process, the concept of a dynamic mechanism was combined to construct an adaptive feature fusion module based on global context information, termed DFF. Subsequently, the DFF module was integrated with MSLK-Block to establish a new feature pyramid structure named DFF-Net.
3) Inspired by the elliptical characteristics of ship targets and the work of Zhou et al. [31], the transformation of the OBB representation into a Gaussian distribution was executed in the prediction head. For the loss calculation, we introduced improved Probabilistic IoU to compute the target regression loss. By measuring the GPD distance, this approach guides the network model's optimization, reducing the imbalance between regression and classification tasks during model learning.

<div align=center>
<img src="https://github.com/SZZ-SXM/MSDFF-Net/blob/main/data/Figure.3 Overall structure - final - 1.png">
</div>
