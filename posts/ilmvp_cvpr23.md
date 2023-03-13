---
layout: paper
title:  "[CVPR23]Understanding and Improving Visual Prompting: A Label-Mapping Perspective"
date: 2023-02-27 21:00:00
author: "<a style='color: #dfebf7' href='https://cse.msu.edu/~chenaoch/'>Aochuan Chen</a><sup>[1]</sup>, 
         <a style='color: #dfebf7' href='https://cse.msu.edu/~yaoyugua/'>Yuguang Yao</a><sup>[1]</sup>, 
         <a style='color: #dfebf7' href='https://sites.google.com/site/pinyuchenpage/home'>Pin-Yu Chen</a><sup>[2]</sup>, 
         <a style='color: #dfebf7' href='https://www.yihua-zhang.com/'>Yihua Zhang</a><sup>[1]</sup>, 
         <a style='color: #dfebf7' href='https://lsjxjtu.github.io/'>Sijia Liu</a><sup>[1,2]</sup>"
maintainer: "<a style='color: #dfebf7' href='https://cse.msu.edu/~chenaoch/'>Aochuan Chen</a>"
affiliation: "<sup>[1]</sup>Michigan State University, <sup>[2]</sup>MIT-IBM Watson AI Lab, IBM Research"
code: "https://github.com/OPTML-Group/ILM-VP"
# poster: ""
paper: "https://arxiv.org/abs/2211.11635"
# slides: ""
---

## Overview

In this paper, we revisit and advance visual prompting (VP) from the perspective of label mapping (LM). we show that when reprogramming an ImageNet-pretrained ResNet-18 to 13 target tasks, our method (ILM-VP) outperforms baselines by a substantial margin, e.g., 7.9% and 6.7% accuracy improvements in transfer learning to the target Flowers102 and CIFAR100 datasets. Besides, our proposal on CLIP-based VP provides 13.7% and 7.1% accuracy improvements on Flowers102 and DTD respectively.

Beyond the significant accuracy gain, we also show the better interpretability brought by our method: The mapped source labels share similar visual features with the target labels. 

<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/ilmvp_cvpr23/overview.png" width="600">
    <br>
    <div style="color:orange;
    display: inline-block;
    color: #999; font-size:16px；
    padding: 2px;">Figure 1. The method of this work and the prior art.</div>
</center>

## Background

The technology of VP addresses the problem of how to adapt a pre-trained source model $f_{\mathbf{\theta}_s}$ (e.g., the ImageNet-1K-pre-trained ResNet-18) to a target downstream task (e.g., flower classification over the Flowers102 dataset) without any task-specific model modification (e.g., finetuning). Throughout the paper, we focus on input-based VP (also known as model reprogramming), which incorporates a carefully-designed universal perturbation pattern to the raw target images so as to enforce the transferability of the source model to the target domain. Although the input prompting operation converts the original image to the source dimension-aligned datapoint that the source model can use, the successful realization of VP needs to map the source model's prediction (in the source label space $\mathcal{Y}_s$ with $K_s$ classes) to the target task's data label (in the target label space $\mathcal{Y}_t$ with $K_t$ classes). Therefore, we ask:

---

<center>
<b>
Given the source model, how to build a mapping from the source label space to the target label space so that the model’s prediction directs to the correct target label?
</b>
<br>
</center>

---

## Existing LM Methods

### Random label mapping (RLM)
RLM does not use any prior knowledge or source model information to guide the LM process. The mapped source labels (to the target domain) could be even random. For example, in the case of 'ImageNet (source) + CIFAR-10 (target)', existing VP  methods coded CIFAR-10 labels using the top 10 ImageNet indices, despite the lack of interpretation. 
### Frequency-based label mapping (FLM)
FLM matches target labels to source labels based on the source model's prediction frequencies on zero-padded target datapoints, i.e., $f_{\mathbf{\theta}_s} ( \mathbf{x}' (\mathbf{\delta}))$ with $\mathbf{\delta} = \mathbf{0}$. More concretely, a target label $y_t$ is mapped to the source label $y_s^*$ following
$$
y_s^* (y_t) = \mathrm{argmax}_{y_s} \mathrm{Pr} \{\text{Top-1 prediction of }f_{\mathbf{\theta}_s}(\mathbf{x}' (\mathbf{0})) \text{ is } y_s | \forall \mathbf{x}_t\in \mathcal{T}_{y_t} \}
$$
where $y_s^* (y_t)$ explicitly expresses the dependence of the mapped source label on the target label, $\mathcal T_{y_t}$ denotes the  target data set in the class $y_t$, and $\mathrm{Pr}\{ \cdot \} $ is the probability of the event that the top-1 prediction of $f_{\mathbf{\theta}_s} $ is  the source class $y_s$ under the zero-padded target data points in $\mathcal{T}_{y_t}$.

As shown in Figure 2, FLM results in a mapping scheme different from that of RLM. However, it is still difficult to interpret the obtained LM results and remains elusive how the quality of LM impacts the performance of VP. 

<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/ilmvp_cvpr23/rlm_flm.png" width="800">
    <br>
    <div style="color:orange;
    display: inline-block;
    color: #999; font-size:16px；
    padding: 2px;">Figure 2. Results of RLM and FLM.</div>
</center>