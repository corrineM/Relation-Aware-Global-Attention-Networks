# Relation-Aware Global Attention (RGA)

## Introduction

Attention mechanisms aim to learn discriminative features. They have been demonstrated useful in many vision tasks. However, many previous works learn the attention using local convolutions with small size receptive fields, ignoring the mining of knowledge from global structure patterns. 
Intuitively, to accurately determine the level of importance of one node, it is better to know the information of all the nodes (for comparison). Motivated by this, we propose an effective Relation-Aware Global Attention (RGA) module which captures the global structural information for better attention learning. Specifically, for each feature position, in order to compactly grasp the structural information of global scope and local appearance information, we propose to stack the relations, i.e., its pairwise correlations/affinities with all the feature positions (e.g., in raster scan order), and the feature itself together to learn the attention with a shallow convolutional model.  

We validate the effectiveness of RGA modules in person re-identification (re-id) task. Our implementation in person re-id is target for the applications of finding lost child, and the visitor density analysis in retail store. 

![image](https://github.com/microsoft/Relation-Aware-Global-Attention-Networks/blob/master/diagrams/spatial_channel_RGA.png)
Figure 1: Diagram of our proposed Spatial Relation-aware Global Attention (RGA-S) and Channel Relation-aware Global Attention (RGA-C). When computing the attention at a feature position, in order to grasp information of global scope, we stack the pairwise relation items, i.e., its correlations/affinities with all the feature positions, and the unary item, i.e., the feature of this position, for learning the attention with convolutional operations. For each feature node, such compact global relation representation contains both affinity and location information and is helpful for learning semantics and infer attention.


## Installation

1. Git clone this repo.
2. Intall dependencies by `pip install -r requirements.txt` (If you hope to use the same environment configuarations as we used for getting the reported results in our paper.)

Sepcifically, we trained all models in our paper on a single NVIDIA Tesla P40 card (with 24GB GPU memory).

## ReID Dataset Preparation
Image-reid datasets (here we use [CUHK03](https://www.cv-foundation.org/openaccess/content_cvpr_2014/papers/Li_DeepReID_Deep_Filter_2014_CVPR_paper.pdf) dataset as an example for description):

1. Create a folder named `cuhk03/` under `/YOUR_DATASET_PATH/`.
2. Download dataset to `/YOUR_DATASET_PATH/cuhk03/` from http://www.ee.cuhk.edu.hk/~xgwang/CUHK_identification.html and extract `cuhk03_release.zip`, so you will have `/YOUR_DATASET_PATH/cuhk03/cuhk03_release`.
3. Download new split from [person-re-ranking](https://github.com/zhunzhong07/person-re-ranking/tree/master/evaluation/data/CUHK03). What you need are `cuhk03_new_protocol_config_detected.mat` and `cuhk03_new_protocol_config_labeled.mat`. Put these two mat files under `data/cuhk03`. Finally, the data structure would look like
```
cuhk03/
    cuhk03_release/
    cuhk03_new_protocol_config_detected.mat
    cuhk03_new_protocol_config_labeled.mat
    ...
```
4. In default mode, we use new split protocol (767/700).
5. *Please remember to modify the variable `DATD_DIR` in our provided bash script for specifying the path of your dataset (`/YOUR_DATASET_PATH/`) accordingly.

## Pre-trained Model Preparation

1. Create a folder named `weights/pre_train` under the root path of this repo.
2. Download the pre-trained ResNet-50 model to `weights/pre_train` from https://download.pytorch.org/models/resnet50-19c8e357.pth.

## Training and Evaluation

For your convenience, we provide the bash script with our recommended hyper-parameters settings. Please `cd` to the root path of this repo and run:

`bash ./scripts/run_rgasc_cuhk03.sh`


## Reference

This technique applied on person re-identification task had been accepted by CVPR'20. 
- [Relation-aware Global Attention for Person Re-identification](https://arxiv.org/pdf/1904.02998.pdf)

We hope this technique of Relation-aware Global Attention to bring benefits for more computer vision tasks and inspire more works.

If you find our paper and repository useful, please cite our paper:

```
@article{zhang2020relation,
  title={Relation-Aware Global Attention for Person Re-identification},
  author={Zhang, Zhizheng and Lan, Cuiling and Zeng, Wenjun and Jin, Xin and Chen, Zhibo},
  journal={CVPR},
  year={2020}
}
```


## Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.opensource.microsoft.com.

When you submit a pull request, a CLA bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., status check, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
