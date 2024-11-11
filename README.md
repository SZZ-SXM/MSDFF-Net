# MSDFF-Net

> [Arbitrary-Direction SAR Ship Detection Method for Multi-Level Imbalanced Problems](Under reviewing)

<!-- [ALGORITHM] -->

## Abstract

Arbitrary-oriented ship detection in SAR imagery facilitates more precise and comprehensive target feature extraction across diverse scenarios. However, achieving optimal detection performance remains challenging due to multi-level imbalances, including object scale imbalance, feature utilization imbalance, and regression loss imbalance. In response to these challenges, this paper presents a Multi-Scale Dynamic Feature Fusion Network (MSDFF-Net), specifically developed for arbitrary-oriented SAR ship detection. First, to lessen impact of scale imbalance impact, a Multi-Scale Large-Kernel Convolution Block (MSLK-Block) is designed, integrating large-kernel with partitioned heterogeneous convolution to enhance the backbone network’s capacity for robust multi-scale feature representation. Second, a Dynamic Feature Fusion Block (DFF-Block) is introduced to optimize spatial and channel-level feature utilization, balancing the contributions of features across different dimensions. Third, to tackle regression loss imbalance, the Gaussian probability distributions (GPD) loss function is designed to account for the elliptical geometry of ship targets. Ablation studies confirm the contribution and efficacy of each component utilized in proposed methodology. Experimental evaluations on the R-SSDD, R-HRSID, and CEMEE datasets demonstrate that MSDFF- reaches top-tier performance standards, outperforming 21 existing deep learning-based SAR ship detectors. Specifically, MSDFF-Net achieves 93.95% precision, 94.72% recall, 91.55% mAP, 94.33% F1-Score, and 135.79 FPS on the R-SSDD dataset, with a parameter size of only 8.94 M. Finally, testing on two large-scale SAR images at different resolutions highlights MSDFF-Net’s strong transferability and deployment capability in real-world maritime scenarios.


