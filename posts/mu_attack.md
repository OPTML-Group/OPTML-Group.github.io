---
layout: paper
title:  "[CVPR'23] Text-Visual Prompting for Efficient 2D Temporal Video Grounding"
date: 2023-05-24 7:00:00
author: 
        "<a style='color: #dfebf7' href='https://damon-demon.github.io'>Yimeng Zhang</a><sup>[1,2]</sup>*, 
        <a style='color: #dfebf7' href='https://jinghanjia.github.io'>Jinghan Jia</a><sup>[1]</sup>*, 
        <a style='color: #dfebf7' href='https://www.linkedin.com/in/xinchenhawaii'>Xin Chen</a><sup>[2]</sup>,
        <a style='color: #dfebf7' href='https://cse.msu.edu/~chenaoch/'>Aochuan Chen</a><sup>[1]</sup>,
        <a style='color: #dfebf7' href='https://www.yihua-zhang.com'>Yihua Zhang</a><sup>[1]</sup>,
        <a style='color: #dfebf7' href='https://scholar.google.com/citations?user=ReWNzl4AAAAJ&hl=en'>Jiancheng Liu</a><sup>[1]</sup>, 
        <a style='color: #dfebf7' href='https://www.linkedin.com/in/dingke'>Ke Ding</a><sup>[2]</sup>,
        <a style='color: #dfebf7' href='https://lsjxjtu.github.io/'>Sijia Liu</a><sup>[1]</sup>"
maintainer: "<a style='color: #dfebf7' href='https://damon-demon.github.io'>Yimeng Zhang</a>"
affiliation: "<sup>[1]</sup>Michigan State University, <sup>[2]</sup>Applied ML, Intel"
code: "https://github.com/OPTML-Group/Diffusion-MU-Attack"
paper: "https://arxiv.org/abs/2310.11868"
---

<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/mu_attack/overview.png" width="1000">
</center>

---

## Abstract

The recent advances in diffusion models (DMs) have revolutionized the generation of complex and diverse images. However, these models also introduce potential safety hazards, such as the production of harmful content and infringement of data copyrights. **Although there have been efforts to create safety-driven unlearning methods to counteract these challenges, doubts remain about their capabilities. To bridge this uncertainty, we propose an evaluation framework built upon adversarial attacks (also referred to as adversarial prompts), in order to discern the trustworthiness of these safety-driven unlearned DMs.** Specifically, our research explores the (worst-case) robustness of unlearned DMs in eradicating unwanted concepts, styles, and objects, assessed by the generation of adversarial prompts. **We develop a novel adversarial learning approach called UnlearnDiff that leverages the inherent classification capabilities of DMs to streamline the generation of adversarial prompts, making it as simple for DMs as it is for image classification attacks. This technique streamlines the creation of adversarial prompts, making the process as intuitive for generative modeling as it is for image classification assaults. Through comprehensive benchmarking, we assess the unlearning robustness of five prevalent unlearned DMs across multiple tasks. Our results underscore the effectiveness and efficiency of UnlearnDiff when compared to state-of-the-art adversarial prompting methods.

**(WARNING: This paper contains model outputs that may be offensive in nature.)**

---

## Our Proposal: Evaluation framework for unlearned diffusion models
Our proposed method for generating adversarial prompts, referred to as the ‘Unlearning Diffusion’ attack (UnlearnDiff). **Unlike previous methods for generating adversarial prompts, we leverage the class-discriminative ability of the ‘diffusion classifier’ inherent in a well-trained DM, using it effectively and without additional costs.** This classification perspective within DMs allows us to craft adversarial prompts exclusively with the victim model (i.e., unlearned DM), eliminating the need for an extra auxiliary DM or image classifier. As a result, our proposal streamlines the diffusion costs during the process of generating attacks.

1. **Turning generation into classification: Exploiting DMs' embedded `free' classifier.**: 
In this work, we will demonstrate that there is no need to introduce an additional DM or classifier because the victim DM inherently serves dual roles  -- image generation and classification.

We next extract the `free' classifier from a DM, referred to as the diffusion classifier \citep{chen2023robust,li2023your}. 
The underlying principle is that classification with a DM can be achieved by applying Bayes' rule to the likelihood of model generation $$p_{\btheta}(\mathbf x | c)$$  and the prior probability distribution  $$p(c)$$ over prompts $$\{ c_i\}$$ (viewed as image `labels'). Following {Sec.\,\ref{sec:problem}}, $$\mathbf x$$ and $$\btheta$$ represent an image and DM's parameters, respectively. 
According to Bayes' rule, the probability of predicting $$\mathbf x$$ as the `label' $c$ is given by

$$
  p_{\btheta}(c_i| \mathbf x) =  \frac{p(c_i) p_{\btheta}(\mathbf x | c_i) }{\sum_j p(c_j) p_{\btheta}(\mathbf x | c_j) },
$$

where $p(c)$ can be a uniform distribution, representing a random guess regarding $$\mathbf{x}$$, while $$p_{\btheta}(\mathbf{x} | c_i)$$ is associated with the quality of image generation corresponding to prompt $c_i$. In the case of the uniform prior, namely, $p(c_i) = p(c_j)$, 
\eqref{eq: condition_prob} can be further simplified to exclusively address the conditional probabilities $$\{ p_{\btheta}(\mathbf x | c_i) \}$$. 
In DM, the log-likelihood of $$p_{\btheta}(\mathbf x | c_i)$$  relates to the denoising error in \eqref{eq: diffusion_training}, \textit{i.e.}, $p_{\btheta}(\mathbf x | c_i) \propto \exp \left \{ -\mathbb{E}_{t, \epsilon }[\| \epsilon - \epsilon_{\boldsymbol \theta}(\mathbf x_t | c_i) \|_2^2] \right \} $, where $\exp{\cdot}$ is the exponential function. 
As a result, the \textit{diffusion classifier} yields

$$
  p_{\btheta}(c_i| \mathbf x) \propto   \frac{  \exp \left \{ -\mathbb{E}_{t, \epsilon}[\| \epsilon - \epsilon_{\boldsymbol \theta}(\mathbf x_t | c_i) \|_2^2] \right \} }{\sum_j  \exp \left \{ -\mathbb{E}_{t, \epsilon }[\| \epsilon - \epsilon_{\boldsymbol \theta}(\mathbf x_t | c_j) \|_2^2] \right \}  }
$$

A key insight is that the DM ($$\btheta$$) can serve as a classifier by evaluating its denoising error for a specific prompt ($c_i$) relative to all the potential errors associated with different prompts.







Inspired by the success of transformers in vision-language tasks, we choose ClipBERT [1](#refer-anchor-1) as the base model for 2D TVG. Extended from ClipBERT, the input of our regression-based TVG model would be describable sentences and uniformly sampled frames of one untrimmed video as shown in figure above. Then, the predicted starting and ending time points of the target video clip would be model outputs.

There are four phases of our proposed TVP framework:

1. **Video frame preprocessing**: We obtain sparsely-sampled frames $$\mathbf{v}_\mathrm{sam}$$
from one input untrimmed video $$\mathbf{v}$$, and apply universal frame-aware visual prompts $$\boldsymbol{\delta}_{\mathrm{vp}}$$ on top of frames at the padding location. 

2. **Feature extraction**: 2D vision encoder (first 5 ConvBlock of ResNet-50) $$g_\mathrm{vid}$$ and language encoder (a trainable word embedding layer) $$g_\mathrm{tex}$$ would extract features from the prompted frames $$\mathbf{v}^{\prime}_\mathrm{sam}$$ and textual inputs $$\mathbf{s}$$, respectively. 

3. **Multimodal feature processing**: Following the setting of Pixel-BERT [2](#refer-anchor-2), the 2D visual features $$\mathbf{Q}_\mathrm{vid}$$ are downsampled spatially by a $$2\times2$$ max-pooling layer and fused temporally by a mean-pooling layer. Then, text prompts $$\boldsymbol{\delta}_{\mathrm{tp}}$$ are integrated into textual features $$\mathbf{Q}_\mathrm{tex}$$. In addition, trainable 2D visual position embeddings $$\mathbf{M}_\mathrm{2D}$$ and textual position embeddings  $$\mathbf{M}_\mathrm{pos}$$ are applied to the processed 2D visual features $$\mathbf{Q}^{\prime}_{\mathrm{vid}}$$ and prompted textual features $$\mathbf{Q}^{\prime}_\mathrm{tex}$$, respectively [1](#refer-anchor-1)[3](#refer-anchor-3).  Afterwards, the processed and position-encoded 2D visual features  $$\mathbf{Q}^{\prime\prime}_{\mathrm{vid}}$$ are flattened and integrated into prompted and position-encoded textual features $$\mathbf{Q}^{\prime\prime}_\mathrm{tex}$$. Moreover, type embeddings $$\mathbf{M}_\mathrm{type}$$ would be added to the integrated multimodal features $$\mathbf{Q}_{\mathrm{all}}$$ to indicate the source type of features.

4. **Crossmodal fusion**: A 12-layer transformer [3](#refer-anchor-3) is utilized for crossmodal fusion on $$\mathbf{Q}_{\mathrm{all}}$$, and then multilayer perceptron (MLP) ending with sigmoid function is used as the prediction head to process the last-layer \underline{c}ross\underline{m}odal representation $$\mathbf{Q}_\mathrm{CM}$$ of the transformer for generating the predicted starting/ending time points $$(\hat{t}_\mathrm{sta}, \hat{t}_\mathrm{sta})$$ of the target moments described by the text query input.


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

<div id="refer-anchor-1"></div>  [2] Huang et al. (2020). Pixel-BERT: Aligning Image Pixels with Text by Deep Multi-Modal Transformers. 

<div id="refer-anchor-1"></div>  [3] Devlin et al. (2018). BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding.
