---
layout: paper
title:  "[CVPR22] Quarantine: Sparsity Can Uncover the Trojan Attack Trigger for Free"
date: 2022-06-21 21:00:00
author_list:
  - name: "Tianlong Chen"
    url: "https://tianlong-chen.github.io/"
    affiliation: "1"
    coauthor: true
  - name: "Zhenyu Zhang"
    url: "https://scholar.google.com/citations?user=ZLyJRxoAAAAJ&hl=zh-CN"
    affiliation: "1"
    coauthor: true
  - name: "Yihua Zhang"
    url: "https://www.yihua-zhang.com/"
    affiliation: "2"
    coauthor: true
  - name: "Shiyu Chang"
    url: "https://code-terminator.github.io/"
    affiliation: "3"
  - name: "Sijia Liu"
    url: "https://lsjxjtu.github.io/"
    affiliation: "2,4"
  - name: "Zhangyang Wang"
    url: "https://vita-group.github.io/"
    affiliation: "1"
affiliation_list:
  - name: "University of Texas at Austin"
  - name: "Michigan State University"
  - name: "University of California, Santa Barbara"
  - name: "MIT-IBM Watson AI Lab"
buttons:
  - text: "Code"
    url: "https://github.com/VITA-Group/Backdoor-LTH"
  - text: "Paper"
    url: "https://arxiv.org/pdf/2205.11819"
  - text: "Poster"
    url: "https://drive.google.com/file/d/1VnnC06NBoRCfSjw2RT91dKCeZ8iDEXCY/view?usp=sharing"
maintainer: "<a href='https://www.yihua-zhang.com'>Yihua Zhang</a>"
---

## Motivation

As models usually learn "too well" during training - so much that make various types of attacks possible, backdoor attack (or Trojan Attack) has become a real-life threat to the AI model deployed in the real world. At the same time, extensive research work on model pruning has shown that the weights of an overparameterized model (e.g., DNN) can be pruned without hampering its generalization ability. Combining both lines of research, our story begins with the following question:

<center>
<b>

How does the model sparsity relate to its train-time robustness against Trojan attacks?

</b>
</center>

## The Discovery of 'Winning Trojan Ticket'

Trojan features learned by backdoored attacks are significantly more stable against pruning than benign features. Therefore, Trojan attacks can be uncovered through the pruning dynamics of the Trojan model.

<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/backdoor_cvpr22/overview.png" width="600">
    <br>
    <div style="color:orange;
    display: inline-block;
    color: #999; font-size:16px；
    padding: 2px;">Figure 1. An overview of our proposal: Weight pruning identifies the ‘winning Trojan ticket’, which can be used for Trojan detection and recovery.</div>
</center>

Leveraging LTH-oriented iterative magnitude pruning (IMP), the ‘winning Trojan Ticket’ can be discovered, which preserves the Trojan attack performance while retaining chance-level performance on clean inputs.

Thus, the existence of the 'winning Trojan Ticket' could serve as an indicator of Trojan attacks. However, in real-world applications, it is hard for the users to acquire the ASR (namely the red curve in Figure 1), as the attack information is transparent to the users. Thus, we need to find a substitute indicator for ASR, which does not require any attack information or even clean data.

The winning Trojan ticket can be detected by our proposed linear model connectivity (LMC)-based Trojan score.

---

## Trojan Score: Linear Mode Connectivity-based Trojan Indicator

We adopt Linear Mode Connectivity [\[2\]](#refer-anchor-2) (LMC) to measure the stability of the Trojan ticket $$\phi := (m \odot \theta)$$ v.s. the $$k$$-step finetuned Trojan ticket $$\phi := (m \odot \theta^{(k)})$$.

We define the Trojan Score as

$$
    \mathcal{S}_{Trojan} = \max_{\alpha \in [0, 1]} \mathcal{E} (\alpha \phi - (1 - \alpha)\phi_{k}) - \frac{\mathcal{\phi} - \mathcal{\phi_k}}{2}
$$

where the first term denotes LMC and the second term an error baseline. $$\mathcal{E}(\phi)$$ denotes the training error of the model $$\phi$$.

A sparse network with the peak Trojan Score maintains the highest ASR in the extreme pruning regime and is termed as the Winning Trojan Ticket.


<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/backdoor_cvpr22/pruning_dynamic.png" width="600">
    <br>
    <div style="color:orange;
    display: inline-block;
    color: #999; font-size:16px；
    padding: 2px;">Figure 2. The pruning dynamics of Trojan ticket (dash line) and 10-step finetuned ticket (solid line) on CIFAR-10 with ResNet-20 and gray-scale backdoor trigger. For comparison, the Trojan score is also reported.</div>
</center>

---

## Backdoor Trigger Reverse Engineering

<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/backdoor_cvpr22/trigger_l1_norm.png" width="1000">
    <br>
    <div style="color:orange; border-bottom: 1px solid #d9d9d9;
    display: inline-block;
    color: #999; font-size:16px；
    padding: 2px;">Figure 3. The \(\ell_1\) norm values of recovered Trojan triggers for all labels. The plot title signifies network architecture, trigger type, and the images for reverse engineering on CIFAR-10. Class “1” is the true target label for Trojan attacks. Green check or red cross indicates whether the detected label (with the least \(\ell_1\) norm matches the true target label).</div>
</center>

---

## Trigger Reverse Engineer

<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/backdoor_cvpr22/recover_trigger_poster.png" width="600">
    <br>
    <div style="color:orange; display: inline-block; color: #999; font-size:16px；padding: 2px;">Figure 4. Visualization of recovered Trojan trigger patterns from dense Trojan models (baseline) and winning Trojan tickets. ResNet-20s on CIFAR-10 with RGB triggers are used. The first column shows the random seed images used for trigger recovery.</div>
</center>

---

## Citation

```
@inproceedings{chen2022quarantine,
  title = {Quarantine: Sparsity Can Uncover the Trojan Attack Trigger for Free},
  author = {Chen, Tianlong and Zhang, Zhenyu and Zhang, Yihua and Chang, Shiyu and Liu, Sijia and Wang, Zhangyang},
  booktitle = {Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition},
  pages = {598--609},
  year = {2022}
}
```
---

## Reference

<div id="refer-anchor-1"></div> [1] Jonathan Frankle et al. “The Lottery Ticket Hypothesis: Finding Sparse, Trainable Neural Networks.” ICLR 2019. 

<div id="refer-anchor-2"></div> [2] Jonathan Frankle et al. “Linear Mode Connectivity and the Lottery Ticket Hypothesis.” ICML 2020.

<div id="refer-anchor-3"></div> [3] Ren Wang et al. “Practical detection of trojan neural networks: Data-limited and data-free cases.” ECCV 2020.
