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

## Label Mapping: ?

Among the many powerful pruning methods, Iterative Magnitude Pruning (IMP) is one of the most significant and popular methods, which prunes the model in an iterative manner and can reach an extremely sparse level without any performance loss. However, it often consumes much more than training a dense model from scratch. In contrast, efficient one-shot pruning methods can not deliver a high-quality sparse subnetwork, as shown in Figure 1.
Therefore, existing pruning methods have reached a dilemma over choosing between the effective method and the efficient method.

<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/bip_nips22/overview.png" width="600">
    <br>
    <div style="color:orange;
    display: inline-block;
    color: #999; font-size:16px；
    padding: 2px;">Figure 1. The dilemma in model pruning: Powerful pruning methods (e.g., IMP) suffer from high computational overhead.</div>
</center>


---

<center>
<b>
Given the source model $f_{\theta_s}$ , how to build a mapping from the source label space $\mathcal{Y}_s$ to the target label space $\mathcal{Y}_t$ so that the model’s prediction directs to the correct target label?
</b>
<br>
</center>

---
