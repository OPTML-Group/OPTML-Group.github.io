---
layout: paper
title:  "[ICLR'24] DeepZero: Scaling up Zeroth-Order Optimization for Deep Model Training"
date: 2024-02-1 7:00:00
author: "<a style='color: #dfebf7' href='https://scholar.google.com/citations?user=7pY-Ie8AAAAJ&hl=en'>Aochuan Chen</a><sup>[1]</sup>*, 
         <a style='color: #dfebf7' href='https://damon-demon.github.io'>Yimeng Zhang</a><sup>[1]</sup>*, 
         <a style='color: #dfebf7' href='https://jinghanjia.github.io/cv/'>Jinghan Jia</a><sup>[1]</sup>, 
         <a style='color: #dfebf7' href='https://people.llnl.gov/diffenderfer2'>James Diffenderfer</a><sup>[2]</sup>,
         <a style='color: #dfebf7' href='https://ljcc0930.github.io'>Jiancheng Liu</a><sup>[1]</sup>, 
         <a style='color: #dfebf7' href='https://people.llnl.gov/parasyris1'>Konstantinos Parasyris</a><sup>[2]</sup>, 
         <a style='color: #dfebf7' href='https://www.yihua-zhang.com'>Yihua Zhang</a><sup>[1]</sup>, 
         <a style='color: #dfebf7' href='https://web.ece.ucsb.edu/~zhengzhang/'>Zheng Zhang</a><sup>[3]</sup>, 
         <a style='color: #dfebf7' href='https://people.llnl.gov/kailkhura1'>Bhavya Kailkhura</a><sup>[2]</sup>, 
         <a style='color: #dfebf7' href='https://lsjxjtu.github.io/'>Sijia Liu</a><sup>[1]</sup>"
maintainer: "<a style='color: #dfebf7' href='https://damon-demon.github.io'>Yimeng Zhang</a>"
affiliation: "<sup>[1]</sup>Michigan State University, <sup>[2]</sup>Lawrence Livermore National Laboratory, <sup>[3]</sup>University of California, Santa Barbara"
code: "https://github.com/OPTML-Group/DeepZero"
paper: "https://arxiv.org/abs/2310.02025"
---

<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/deepzero_iclr24/deepzero_iclr24.png" width="1500">
</center>

Overview of our DeepZero framework.

---

## Abstract

Zeroth-order (ZO) optimization has become a popular technique for solving machine learning (ML) problems when first-order (FO) information is difficult or impossible to obtain. However, the scala- bility of ZO optimization remains an open problem: Its use has primarily been limited to relatively small-scale ML problems, such as sample-wise adversarial attack generation. To our best knowl- edge, no prior work has demonstrated the effectiveness of ZO optimization in training deep neural networks (DNNs) without a significant decrease in performance. To overcome this roadblock, we develop DeepZero, a principled ZO deep learning (DL) framework that can scale ZO optimization to DNN training from scratch through three primary innovations. First, we demonstrate the advantages of coordinate-wise gradient estimation (CGE) over randomized vector-wise gradient estimation in training accuracy and computational efficiency. Second, we propose a sparsity-induced ZO training protocol that extends the model pruning methodology using only finite differences to explore and exploit the sparse DL prior in CGE. Third, we develop the methods of feature reuse and forward parallelization to advance the practical implementations of ZO training. Our extensive experiments show that DeepZero achieves state-of-the-art (SOTA) accuracy on ResNet-20 trained on CIFAR-10, approaching FO training performance for the first time. Furthermore, we show the practical utility of DeepZero in applications of certified adversarial defense and DL-based partial differential equa- tion error correction, achieving 10-20% improvement over SOTA. We believe our results will inspire future research on scalable ZO optimization and contribute to advancing DL with black box.

---

## Motivations: Why Zeroth-Order (ZO) Optimization needed for model training?

## Challenges: High Computation Cost

## Contributions

## ZO Gradient Estimator: RGE or CGE?

## Proposed ZO Training Framework





Inspired by the success of transformers in vision-language tasks, we choose ClipBERT [[1](#refer-anchor-1)] as the base model for 2D TVG. Extended from ClipBERT, the input of our regression-based TVG model would be describable sentences and uniformly sampled frames of one untrimmed video as shown in figure above. Then, the predicted starting and ending time points of the target video clip would be model outputs.

There are four phases of our proposed TVP framework:

1. **Video frame preprocessing**: We obtain sparsely-sampled frames $$\mathbf{v}_\mathrm{sam}$$
from one input untrimmed video $$\mathbf{v}$$, and apply universal frame-aware visual prompts $$\boldsymbol{\delta}_{\mathrm{vp}}$$ on top of frames at the padding location. 

2. **Feature extraction**: 2D vision encoder (first 5 ConvBlock of ResNet-50) $$g_\mathrm{vid}$$ and language encoder (a trainable word embedding layer) $$g_\mathrm{tex}$$ would extract features from the prompted frames $$\mathbf{v}^{\prime}_\mathrm{sam}$$ and textual inputs $$\mathbf{s}$$, respectively. 

3. **Multimodal feature processing**: Following the setting of Pixel-BERT [[2](#refer-anchor-2)], the 2D visual features $$\mathbf{Q}_\mathrm{vid}$$ are downsampled spatially by a $$2\times2$$ max-pooling layer and fused temporally by a mean-pooling layer. Then, text prompts $$\boldsymbol{\delta}_{\mathrm{tp}}$$ are integrated into textual features $$\mathbf{Q}_\mathrm{tex}$$. In addition, trainable 2D visual position embeddings $$\mathbf{M}_\mathrm{2D}$$ and textual position embeddings  $$\mathbf{M}_\mathrm{pos}$$ are applied to the processed 2D visual features $$\mathbf{Q}^{\prime}_{\mathrm{vid}}$$ and prompted textual features $$\mathbf{Q}^{\prime}_\mathrm{tex}$$, respectively [[1](#refer-anchor-1), [3](#refer-anchor-3)].  Afterwards, the processed and position-encoded 2D visual features  $$\mathbf{Q}^{\prime\prime}_{\mathrm{vid}}$$ are flattened and integrated into prompted and position-encoded textual features $$\mathbf{Q}^{\prime\prime}_\mathrm{tex}$$. Moreover, type embeddings $$\mathbf{M}_\mathrm{type}$$ would be added to the integrated multimodal features $$\mathbf{Q}_{\mathrm{all}}$$ to indicate the source type of features.

4. **Crossmodal fusion**: A 12-layer transformer [[3](#refer-anchor-3)] is utilized for crossmodal fusion on $$\mathbf{Q}_{\mathrm{all}}$$, and then multilayer perceptron (MLP) ending with sigmoid function is used as the prediction head to process the last-layer \underline{c}ross\underline{m}odal representation $$\mathbf{Q}_\mathrm{CM}$$ of the transformer for generating the predicted starting/ending time points $$(\hat{t}_\mathrm{sta}, \hat{t}_\mathrm{sta})$$ of the target moments described by the text query input.


---

## Performance Comparison
Our method yields substantial accuracy improvement on multiple datasets.

<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/2dtvp_cvpr23/performance_table.png" width="1200">
    <br>
    <div style="color:orange;
    display: inline-block;
    color: #999; font-size:2px；
    padding: 2px;">Performance comparison of different thresholds m on the Charades-STA and ActivityNet Captions Datasets.</div>
</center> 


---

## Citation
```
@article{zhang2023text,
  title={Text-visual prompting for efficient 2d temporal video grounding},
  author={Zhang, Yimeng and Chen, Xin and Jia, Jinghan and Liu, Sijia and Ding, Ke},
  journal={arXiv preprint arXiv:2303.04995},
  year={2023}
}
```

---

## References

<div id="refer-anchor-1"></div>  [1] Lei et al. (2021). Less is More: ClipBERT for Video-and-Language Learning via Sparse Sampling. 

<div id="refer-anchor-2"></div>  [2] Huang et al. (2020). Pixel-BERT: Aligning Image Pixels with Text by Deep Multi-Modal Transformers. 

<div id="refer-anchor-3"></div>  [3] Devlin et al. (2018). BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding.
