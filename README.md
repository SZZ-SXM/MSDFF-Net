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

## Experimental Dataset

1) The SSDD [28] is the inaugural dataset explicitly created for detecting ship targets in SAR imagery, featuring both HBB and OBB annotation formats. This dataset comprises images from three radar satellites: RadarSat-2, TerraSAR-X, and Sentinel-1, which offers resolutions that vary between 1 and 15 meters. Ship targets are distributed across offshore and inshore scenes. The original dataset includes 1160 images and 2456 ship instances, with image sizes ranging from 190 to 688 pixels. To standardize the input image dimensions, the original dataset was processed to resize all images to 512×512 pixels, which yields in altogether 1247 images (872 images are assigned to training, while 375 are used for testing). Additionally, the annotations of this dataset were revised based on expert experience, yielding the R-SSDD used in our experiments. The R-SSDD contains a total of 2853 ship instances (1975 for training and 878 for testing).
2) The HRSID [29] represents the initial dataset specifically designed for high-resolution SAR ship instance segmentation, featuring HBB and Mask annotation formats. This dataset is composed of images from satellites including Sentinel-1B, TerraSAR-X, and TanDEM-X, with resolutions varying from 0.5 to 3 meters. Ship targets are distributed across offshore and inshore scenes. The original dataset consists of 5604 images and 16951 ship instances, with each image sized at 800×800 pixels. The Mask annotations of this dataset were converted to OBB annotations, and the annotations were further revised based on expert experience, resulting in the R-HRSID used in our experiments. The R-HRSID contains a total of 16956 ship instances (11038 for training and 5918 for testing).
3) The CEMEE [30] dataset is an open dataset from the 8th CEMEE Cup Electromagnetic Environment Mathematical Modeling Detection and Recognition Algorithm Challenge, featuring OBB annotation format. This dataset consists entirely of images from the Gaofen-3 radar satellite, with a resolution of 1 meter. Ship targets are distributed across offshore and inshore scenes. After manual correction, the dataset contains 1500 images of size 1024x1024 pixels (1000 for training and 500 for testing), with a total of 7254 ship instances (4,822 images are designated for training, while 2,432 images are allocated for testing). And original CEMEE dataset have seven categories (S1-S7), for our experiments, all categories were merged into a single "ship" class to focus on detection performance.

All calibration data mentioned above can be accessed via the Baidu Netdisk link: https://github.com/SZZ-SXM/MSDFF-Net/blob/main/data/.

## Visualization result
In addition to optimizing the feature extraction module, the proposed algorithm also improves the feature fusion process. By incorporating a dynamic fusion mechanism, features extracted from different layers of backbone model are dynamically integrated using our DFF-Net, effectively enhancing the semantic association between global and local scene information. To assess the efficacy of our feature fusion approach, we performed a visual analysis of the fused features using Eigen-CAM [37]. Eigen-CAM generates multi-scale class activation maps (CAM) from feature maps at different levels and can be directly applied to pre-trained models, making it highly suitable for validating the feasibility of DFF-Net structure.

<div align=center>
<img src="https://github.com/SZZ-SXM/MSDFF-Net/blob/main/data/Fig.10 DFF-Net有效性验证.png">
</div>

## Quantitative result
To comprehensively showcase the viability of our proposed MSDFF-Net, a thorough comparative with 21 DL-based OBB detection algorithms conducted in this section. These 21 detection algorithms are categorized into three main groups, including four anchor-free detection methods: CFA [38], Oriented RepPoints [39], Rotated RepPoints [40], and SASM RepPoints [41]; five two-stage detection methods: Faster-RCNN-OBB [13], Gliding Vertex [42], Oriented R-CNN [43], ReDet [44], and RoI Transformer [45]; and twelve single-stage detection methods: ATSS-OBB [46], ConvNeXt [47], CSL [48], FCOS-OBB [49], GWD [50], KFIoU [51], KLD [52], PSC [53], R3Det [54], RetinaNet-OBB [55], RTMDet-OBB [36], and S2ANet [56]. All these algorithms were implemented within the same Pytorch-based mmrotate framework [36] to ensure the accuracy of the comparisons. Additionally, all methods were evaluated under the same software and hardware environment.

<div align=center>
<img src="https://github.com/SZZ-SXM/MSDFF-Net/blob/main/data/0Quantitative result.jpg">
</div>

**Note**:

1. We follow the latest metrics from the DOTA evaluation server, original voc format mAP is now mAP50.
2. All of our experiments were conducted in the same setting for easy model comparison.
3. All experiments were conducted using PyTorch 1.12.1, CUDA 11.6, and CuDNN 8.3.2, with an Intel(R) Xeon(R) Gold 6139 CPU operating at 2.30 GHz and a single NVIDIA GeForce RTX 3090 GPU.

## Contact
Welcome to raise issues or email to sunzhongzhen14@163.com or sunzhongzhen14@nudt.edu.cn for any question regarding our MSDFF-Net.

## Citation

```
@misc{szz2024MSDFF-Net,
      title={Arbitrary-Direction SAR Ship Detection Method for Multi-Level Imbalanced Problems},
      author={Zhongzhen Sun, Xiangguang Leng, Member, IEEE, Xianghui Zhang, Zheng Zhou, Boli Xiong, Kefeng Ji, Member, IEEE, and Gangyao Kuang, Senior Member, IEEE},
      year={2024},
      primaryClass={under reviewing in TGRS}
}
```
