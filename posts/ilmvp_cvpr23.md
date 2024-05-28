---
layout: paper
title:  "[CVPR23] Understanding and Improving Visual Prompting: A Label-Mapping Perspective"
date: 2023-02-27 21:00:00
author_list:
  - name: "Aochuan Chen"
    url: "https://cse.msu.edu/~chenaoch/"
    affiliation: "1"
  - name: "Yuguang Yao"
    url: "https://cse.msu.edu/~yaoyugua/"
    affiliation: "1"
  - name: "Pin-Yu Chen"
    url: "https://sites.google.com/site/pinyuchenpage/home"
    affiliation: "2"
  - name: "Yihua Zhang"
    url: "https://www.yihua-zhang.com/"
    affiliation: "1"
  - name: "Sijia Liu"
    url: "https://lsjxjtu.github.io/"
    affiliation: "1,2"
affiliation_list:
  - name: "Michigan State University"
  - name: "MIT-IBM Watson AI Lab, IBM Research"
buttons:
  - text: "Code"
    url: "https://github.com/OPTML-Group/ILM-VP"
  - text: "Paper"
    url: "https://arxiv.org/abs/2211.11635"
---

<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/ilmvp_cvpr23/overview.png" width="1200">
</center>

Existing label mapping methods seem ruleless? We intertwine the VP dynamic and the label mapping to boost the performance and interpretability of VP.

---

## Abstract

We revisit and advance visual prompting (VP), an input prompting technique for vision tasks. VP can reprogram a fixed, pre-trained source model to accomplish downstream tasks in the target domain by simply incorporating universal prompts (in terms of input perturbation patterns) into downstream data points. Yet, it remains elusive why VP stays effective even given a ruleless label mapping (LM) between the source classes and the target classes. Inspired by the above, we ask: How is LM interrelated with VP? And how to exploit such a relationship to improve its accuracy on target tasks? We peer into the influence of LM on VP and provide an affirmative answer that a better 'quality' of LM (assessed by mapping precision and explanation) can consistently improve the effectiveness of VP. This is in contrast to the prior art where the factor of LM was missing. To optimize LM, we propose a new VP framework, termed ILM-VP (iterative label mapping-based visual prompting), which automatically re-maps the source labels to the target labels and progressively improves the target task accuracy of VP. Further, when using a contrastive language-image pretrained (CLIP) model, we propose to integrate an LM process to assist the text prompt selection of CLIP and to improve the target task accuracy. Extensive experiments demonstrate that our proposal significantly outperforms state-of-the-art VP methods. As highlighted below, we show that when reprogramming an ImageNet-pretrained ResNet-18 to 13 target tasks, our method outperforms baselines by a substantial margin, e.g., 7.9% and 6.7% accuracy improvements in transfer learning to the target Flowers102 and CIFAR100 datasets. Besides, our proposal on CLIP-based VP provides 13.7% and 7.1% accuracy improvements on Flowers102 and DTD respectively.

---

## Why Label Mapping Matters?
VP is an emerging technique for transfer learning which needs an input perturbation pattern and a label mapping strategy. However, although the SOTA label mapping method (frequency label mapping, FLM) improves performance over the random label mapping (RLM) method, it fails to deliver clear interpretability. It is worth noting that the updating of VP pattern induces prediction dynamics, which leads to the inconsistency between pre- and post-prompt prediction frequency.

<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/ilmvp_cvpr23/rlm_flm.png" width="1200">
    <br>
    <div style="color:orange;
    display: inline-block;
    color: #999; font-size:2px；
    padding: 2px;">Visualizations of RLM and FLM. In FLM, the post-prompt label mapping shows many newly-selected source labels, indicating the dynamics of LM in the source domain, and the pre-prompt LM is sub-optimal (i.e., mis-selecting the best-matching label) after VP training.</div>
</center>

---

## Our Proposal: ILM-VP
We propose to take the LM dynamics into the prompt learning process. Namely, we alternatively optimize the VP pattern and the LM strategy.

<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/ilmvp_cvpr23/alg.png" width="1200">
    <br>
    <div style="color:orange;
    display: inline-block;
    color: #999; font-size:2px；
    padding: 2px;">ILM-VP algorithm.</div>
</center>

---

## Performance Boost
Our method yields substantial accuracy improvement on multiple datasets.

<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/ilmvp_cvpr23/main_table.png" width="1200">
    <br>
    <div style="color:orange;
    display: inline-block;
    color: #999; font-size:2px；
    padding: 2px;">RLM-VP: Vanilla Visual Prompting using Random Label Mapping in [Bahng, et al., 2022], FLM-VP: Advanced Visual Prompting using Frequency Label Mapping in [Tsai, et al., 2020], LP: Linear Probing (finetuning the classification head), FF: Full Finetuning (finetuning the whole model).</div>
</center>

---

## Interpretability Merit

Our method unveils source-target label pairs that share similar features in the vision domain.

<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/ilmvp_cvpr23/ebe.png" width="1200">
</center>

---

## Discussion
As shown in our table, VP-based transfer learning has not been able to outperform LP and FF in many datasets. Thus, it is an open challenge how to further boost the effectiveness of pixel-level VP in CNN-based models. However, we would like to stress that VP is still a very interesting ideas for vision models as it enjoys parameter efficiency, in particular when facing numerous downstream tasks: VP-type methods only take 0.05M input parameters per task while LP and FF require 0.5M and more than 10M task-specific model parameters, respectively. What’s more, a smaller parameter space may require less downstream data in transfer learning. For example, VP yields a significant improvement over FF on the ABIDE dataset (with an extremely small dataset size). In addition, VP has the potential to achieve transfer learning under black-box source models, where prompts can be learned using model queries [Tsai, et al., 2020]. Considering the emergent foundation models, the black-box design of VP for these models remains important and very useful to users. 

---

## Acknowledgement

The work of A. Chen, Y. Yao, Y. Zhang, and S. Liu was supported by the DARPA RED program and National Science Foundation (NSF) Grant IIS-2207052.

---

## Citation
```
@article{chen2022understanding,
  title={Understanding and Improving Visual Prompting: A Label-Mapping Perspective},
  author={Chen, Aochuan and Yao, Yuguang and Chen, Pin-Yu and Zhang, Yihua and Liu, Sijia},
  journal={arXiv preprint arXiv:2211.11635},
  year={2022}
}
```

---

## References

[1] Bahng, Hyojin, et al. "Visual prompting: Modifying pixel space to adapt pre-trained models." arXiv preprint arXiv:2203.17274 (2022).

[2] Tsai, Yun-Yun, Pin-Yu Chen, and Tsung-Yi Ho. "Transfer learning without knowing: Reprogramming black-box machine learning models with scarce data and limited resources." International Conference on Machine Learning. PMLR, 2020.
