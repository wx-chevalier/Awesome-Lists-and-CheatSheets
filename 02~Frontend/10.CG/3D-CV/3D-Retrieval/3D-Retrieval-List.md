# 3D Retrieval List

# Paper

- [2012-3D Shape Retrieval from a 2D Image as Query](http://www.apsipa.org/proceedings_2012/papers/19.pdf): In this paper, we propose a new method for defining a feature vector for 3D shape retrieval from a single 2D photo image. Our feature vector is defined as a combination of Zernike moments and HOG (Histogram of Oriented Gradients), where these features can be extracted from both a 2D image and a 3D shape model.

- [2020~An Efficient 3D Model Retrieval Method Based on Convolutional Neural Network #Paper#](https://www.hindawi.com/journals/complexity/2020/9050459/): In this paper, we propose a method to extract 2D representative views. In this method, the K-means is adopted to classify views into different categories according to their similarity, and then one representative view is chosen from each category. In this way, different 3D models may yield different numbers of 3D views.

- [2023~Self-supervised Image-based 3D Model Retrieval #Paper#](https://dl.acm.org/doi/10.1145/3548690): In this article, besides utilizing the label information of 2D image domain and the adversarial domain alignment, we additionally incorporate self-supervision to address cross-domain 3D model retrieval problem.

- [2023~3D model retrieval based on interactive attention CNN and multiple features #Paper#](https://peerj.com/articles/cs-1227/): In this article, we combine semantic feature, shape distribution features and gist feature to retrieve 3D model based on interactive attention convolutional neural networks (CNN).

# OpenSource

## Classification

- [2015-mvcnn ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/suhangpro/mvcnn)](https://github.com/suhangpro/mvcnn): The goal of the project is to learn a general purpose descriptor for shape recognition. To do this we train discriminative models for shape recognition using convolutional neural networks (CNNs) where view-based shape representations are the only cues. Examples include line-drawings, clip art images where color is removed, or renderings of 3D models where there is little or no texture information present.

  - [mvcnn_pytorch](https://github.com/jongchyisu/mvcnn_pytorch)

- [2016-Pointnet ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/charlesq34/pointnet)](https://github.com/charlesq34/pointnet): Deep Learning on Point Sets for 3D Classification and Segmentation.

- [2018-3D-shape-retrieval ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/sijia3/3D-shape-retrieval)](https://github.com/sijia3/3D-shape-retrieval): 针对三维模型检索，并采用卷积神经网络，提出两个算法：1.采用体素化深层特征进行训练。2. 采用虚拟摄像机抓取多角度视图特征进行训练。

- [2020~CADNet ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/AndrewColligan/CADNet)](https://github.com/AndrewColligan/CADNet): Code for Graph Representation of 3D CAD models for Machining Feature Recognition with Deep Learning paper. This is an approach using graph neural networks to learning from planar B-Rep CAD models. In the paper, focus was given towards the machining feature recognition task. Here, faces in B-Rep models were classified as different machining feature classes.

- [2021~MVTN ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/ajhamdi/MVTN)](https://github.com/ajhamdi/MVTN): MVTN learns to transform the rendering parameters of a 3D object to improve the perspectives for better recognition by multi-view netowkrs. Without extra supervision or add loss, MVTN improve the performance in 3D classification and shape retrieval. MVTN achieves state-of-the-art performance on ModelNet40, ShapeNet Core55, and the most recent and realistic ScanObjectNN dataset (up to 6% improvement).

- [2021~IBSR_jittor ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/IGLICT/IBSR_jittor)](https://github.com/IGLICT/IBSR_jittor): Code for 'Single Image 3D Shape Retrieval via Cross-Modal Instance and Category Contrastive Learning', ICCV 2021

- [2020~Extract-Features-from-3D-meshes-for-Machine-Learning ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/IvanNik17/Extract-Features-from-3D-meshes-for-Machine-Learning)](https://github.com/IvanNik17/Extract-Features-from-3D-meshes-for-Machine-Learning): Two Python scripts for extracting hand crafted features from 3D meshes and point clouds for Machine Learning. Features have been used as data for Random Forests, AdaBoost, Descision Trees, etc.

- [2020~shrec21-3d-mesh-retrieval ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/kaylode/shrec21-3d-mesh-retrieval)](https://github.com/kaylode/shrec21-3d-mesh-retrieval): Object retrieval and classification networks trained directly on the 3D objects in mesh form.

- [2022~3D_STEP_Classification ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/divanoLetto/3D_STEP_Classification)](https://github.com/divanoLetto/3D_STEP_Classification): A new approach for retrieval and classification of 3D models that directly performs in the CAD format without any format conversion to other representations like point clouds of meshes, thus avoiding any loss of information.

- [2022~ROCA ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/cangumeli/ROCA)](https://github.com/cangumeli/ROCA): Official code for ROCA: Robust CAD Model Retrieval and Alignment from a Single Image (CVPR 2022)
