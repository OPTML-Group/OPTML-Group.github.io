---
layout: paper
title:  "[ICML22]Revisiting and Advancing Fast Adversarial Training Through The Lens of Bi-Level Optimization"
date: 2022-07-28 21:00:00
author_list:
  - name: "Yihua Zhang"
    url: "https://www.yihua-zhang.com/"
    affiliation: "1"
    coauthor: true
  - name: "Guanhua Zhang"
    url: "https://https://ghzhang233.github.io/"
    affiliation: "2"
    coauthor: true
  - name: "Prashant Khanduri"
    url: "https://sites.google.com/view/khanduri-prashant/home"
    affiliation: "3"
    coauthor: true
  - name: "Mingyi Hong"
    url: "https://people.ece.umn.edu/~mhong/mingyi.html"
    affiliation: "3"
  - name: "Shiyu Chang"
    url: "https://code-terminator.github.io/"
    affiliation: "1"
  - name: "Sijia Liu"
    url: "https://lsjxjtu.github.io/"
    affiliation: "2,4"
affiliation_list:
  - name: "Michigan State University"
  - name: "University of California, Santa Barbara"
  - name: "University of Minnesota"
  - name: "MIT-IBM Watson AI Lab"
buttons:
  - text: "Code"
    url: "https://github.com/OPTML-Group/Fast-BAT"
  - text: "Paper"
    url: "https://proceedings.mlr.press/v162/zhang22ak/zhang22ak.pdf"
  - text: "Poster"
    url: "https://drive.google.com/file/d/1hPXqvVt-nXymYK8Rc3bk-mFYmVbEEard/view?usp=sharing"
  - text: "Slides"
    url: "https://drive.google.com/file/d/13uI2Uzl_yLNdx2o1QqjGiQWFmL8RLaCn/view?usp=sharing"
maintainer: "<a href='https://www.yihua-zhang.com'>Yihua Zhang</a>"
---

## Motivation

Adversarial training (AT) is a widely recognized defense mechanism to gain the robustness of deep neural networks against adversarial attacks. However, the conventional MMO method makes AT hard to scale. Thus, Fast-AT and other recent algorithms attempt to simplify MMO by replacing its maximization step with the single gradient sign-based attack generation step. Although easy to implement, FAST-AT lacks theoretical guarantees, and its empirical performance is unsatisfactory due to the issue of robust catastrophic overfitting when training with strong adversaries.  Moreover, there has been no theoretical guarantee for the optimization algorithms used in FAST-AT. Given the limitations, we ask:

<center>
<b>

How to design a ‘fast’ AT with improved stability,
mitigated catastrophic overfitting,
and theoretical guarantees?

</b>
</center>

<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/fastbat_icml22/overview.png" width="600">
    <br>
    <div style="color:orange;
    display: inline-block;
    color: #999; font-size:16px；
    padding: 2px;">Figure 1. An overview of our proposal: Adversarial training through bi-level optimization (BLO). The </div>
</center>


## Fast Robust Training: Not Enough!



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
