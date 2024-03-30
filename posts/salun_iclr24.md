---
layout: paper
title:  "[ICLR24 Spotlight] SalUn: Empowering Machine Unlearning via Gradient-based Weight Saliency in Both Image Classification and Generation"
date: 2024-03-15 21:00:00
author: "<a style='color: #dfebf7' href='https://a-f1.github.io/'>Chongyu Fan</a><sup>[1]</sup>*,
         <a style='color: #dfebf7' href='https://ljcc0930.github.io/'>Jiancheng Liu</a><sup>[1]</sup>*,
         <a style='color: #dfebf7' href='https://www.yihua-zhang.com/'>Yihua Zhang</a><sup>[1]</sup>,
         <a style='color: #dfebf7' href='https://riceric22.github.io/'>Eric Wong</a><sup>[2]</sup>,
         <a style='color: #dfebf7' href='https://sites.google.com/site/dennislwei/'>Dennis Wei</a><sup>[3]</sup>,
         <a style='color: #dfebf7' href='https://lsjxjtu.github.io/'>Sijia Liu</a><sup>[1,3]</sup>"
affiliation: "<sup>[1]</sup>Michigan State University, <sup>[2]</sup>University of Pennsylvania, <sup>[3]</sup>IBM Research"
code: "https://github.com/OPTML-Group/Unlearn-Saliency"
# poster: ""
paper: "https://arxiv.org/pdf/2310.12508.pdf"
---
<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/salun_iclr24/teaser-v2.png" width="800">
    <br>
    <div style="color:orange;
    display: inline-block;
    color: #999; font-size:16px；
    padding: 2px;">
    Figure 1: Schematic overview of our proposal on Saliency Unlearning (SalUn).</div>
</center>

--- 

## Abstract


With evolving data regulations, machine unlearning (MU) has become an important tool for fostering trust and safety in today's AI models. However, existing MU methods focusing on data and/or weight perspectives often suffer limitations in unlearning accuracy, stability, and cross-domain applicability. To address these challenges, we introduce the concept of 'weight saliency' for MU, drawing parallels with input saliency in model explanation. This innovation directs MU's attention toward specific model weights rather than the entire model, improving effectiveness and efficiency. The resultant method that we call saliency unlearning (SalUn) narrows the performance gap with 'exact' unlearning (model retraining from scratch after removing the forgetting data points). To the best of our knowledge, SalUn is the first principled MU approach that can effectively erase the influence of forgetting data, classes, or concepts in both image classification and generation tasks. As highlighted below, For example, SalUn yields a stability advantage in high-variance random data forgetting, *e.g.*, with a 0.2% gap compared to exact unlearning on the CIFAR-10 dataset. Moreover, in preventing conditional diffusion models from generating harmful images, SalUn achieves nearly 100% unlearning accuracy, outperforming current state-of-the-art baselines like Erased Stable Diffusion and Forget-Me-Not.

**WARNING**: This paper contains model outputs that may be offensive in nature.

---


## Acknowledgement

C. Fan, J. Liu, and S. Liu were supported by the Cisco Research Faculty Award and the National Science Foundation (NSF) Robust Intelligence (RI) Core Program Award IIS-2207052.

---

## Citation
```
@article{fan2023salun,
  title={Salun: Empowering machine unlearning via gradient-based weight saliency in both image classification and generation},
  author={Fan, Chongyu and Liu, Jiancheng and Zhang, Yihua and Wei, Dennis and Wong, Eric and Liu, Sijia},
  journal={arXiv preprint arXiv:2310.12508},
  year={2023}
}
```