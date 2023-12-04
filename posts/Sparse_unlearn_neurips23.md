---
layout: paper
title:  "[NeurIPS23] Model Sparsity Can Simplify Machine Unlearning"
date: 2023-12-02 21:00:00
author: "<a style='color: #dfebf7' href='https://jinghanjia.netlify.app'>Jinghan Jia</a><sup>[1]</sup>*,
         <a style='color: #dfebf7' href='https://scholar.google.com/citations?user=ReWNzl4AAAAJ&hl=en'>Jiancheng Liu</a><sup>[1]</sup>*,
         <a style='color: #dfebf7' href='https://rithram.github.io/'>Parikshit Ram</a><sup>[2]</sup>,
         <a style='color: #dfebf7' href='https://www.cse.msu.edu/~yaoyugua/'>Yuguang Yao</a><sup>[1]</sup>,
         <a style='color: #dfebf7' href='https://www.linkedin.com/in/gaowen-liu-1b52a610a/'>Gaowen Liu</a><sup>[3]</sup>,
         <a style='color: #dfebf7' href='http://www.yliuu.com/'>Yang Liu</a><sup>[4,5]</sup>,
         <a style='color: #dfebf7' href='https://sites.google.com/view/pranay-sharma/home'>Pranay Sharma</a><sup>[6]</sup>,
         <a style='color: #dfebf7' href='https://lsjxjtu.github.io/'>Sijia Liu</a><sup>[1,2]</sup>"
affiliation: "<sup>[1]</sup>Michigan State University, <sup>[2]</sup>IBM Research, <sup>[3]</sup>Cisco Research, <sup>[4]</sup>University of California, Santa Cruz, <sup>[5]</sup>ByteDance Research, <sup>[6]</sup>Carnegie Mellon University"
code: "https://github.com/OPTML-Group/Unlearn-Sparse"
poster: "https://jinghanjia.netlify.app/assets/img/publication_preview/unlearn-sparse"
paper: "https://arxiv.org/pdf/2304.04934.pdf"
categories: "neurips23"
---
<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/Sparse_unlearn_neurips23/overview.png" width="800">
    <br>
    <div style="color:orange;
    display: inline-block;
    color: #999; font-size:16px；
    padding: 2px;">
    Figure 1: Enhancing Machine Unlearning: Bridging the Performance Gap with Model Sparsity.</div>
</center>

--- 

## Abstract

In response to recent data regulation requirements, machine unlearning (MU) has
emerged as a critical process to remove the influence of specific examples from a
given model. Although exact unlearning can be achieved through complete model
retraining using the remaining dataset, the associated computational costs have
driven the development of efficient, approximate unlearning techniques. Moving
beyond data-centric MU approaches, our study introduces a novel model-based
perspective: model sparsification via weight pruning, which is capable of reducing
the gap between exact unlearning and approximate unlearning. We show in both
theory and practice that model sparsity can boost the multi-criteria unlearning
performance of an approximate unlearner, closing the approximation gap, while
continuing to be efficient. This leads to a new MU paradigm, termed prune first,
then unlearn, which infuses a sparse model prior into the unlearning process.
Building on this insight, we also develop a sparsity-aware unlearning method that
utilizes sparsity regularization to enhance the training process of approximate
unlearning. Extensive experiments show that our proposals consistently benefit
MU in various unlearning scenarios. A notable highlight is the 77% unlearning
efficacy gain of fine-tuning (one of the simplest unlearning methods) when using
sparsity-aware unlearning. Furthermore, we demonstrate the practical impact of
our proposed MU methods in addressing other machine learning challenges, such
as defending against backdoor attacks and enhancing transfer learning. 

---

## What is Machine Unlearning?

**Machine unlearning (MU)**: Erase influence of specific data/classes in model performance, e.g., to comply with data privacy regulations [Cao, et al., 2015]. 

<div style="display: flex; justify-content: space-around; align-items: center;">
  <div style="margin-right: 10px; text-align: center;"><img src="{{ site.url }}{{ site.baseurl }}/images/postpic/Sparse_unlearn_neurips23/pretrain.png" alt="Pretrained Model" style="width: 100%;"/>
<p>Pretrained Model</p>
  </div>
  <div style="margin-left: 10px; text-align: center;"><img src="{{ site.url }}{{ site.baseurl }}/images/postpic/Sparse_unlearn_neurips23/unlearn.png" alt="Unlearned Model" style="width: 100%;"/>
<p>Unlearned Model</p>
  </div>
</div>
<center>
Figure 2: Overview for Machine Unlearning.
</center>

---



## What are Challenges in Machine Unlearning?
**Efficicy Challenge**: The optimal machine unlearning (MU) strategy requires retraining the model from scratch over retaining dataset (after removing data points to be unlearned). But it lacks training efficiency, particularly for large-scale deep models. Hence, there's a need for **fast**, yet **effective** MU methods.

**Evaluation Challenges**: 

Different from traditional machine learning problem, MU requires multiple unlearning performance metrics, which shown in the figure 3 below.
<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/Sparse_unlearn_neurips23/evaluation.png" width="800">
    <br>
    <div style="color:orange;
    display: inline-block;
    color: #999; font-size:16px；
    padding: 2px;">
    Figure 3: Three Evaluation Dimensions for Machine Unlearning</div>
</center>
---

## Model Sparsity Helps Unlearning!
The fundamental insight behind employing model pruning lies in the reduction of the unlearning dimensions and the associated unlearning error. This reduction refers to the disparity between approximate unlearning and exact unlearning, the latter achieved by retraining the model from scratch. In our work, we extend the analytical framework of Thudi et al. regarding machine unlearning to encompass sparse models. **Proposition 2** of our paper elucidates that an increase in model sparsity, as indicated by the sparsity pattern $$m$$, contributes to a decrease in the unlearning error. Nonetheless, it is critical to acknowledge that operating within a regime of high sparsity may inversely affect the model’s capacity for generalization.
<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/Sparse_unlearn_neurips23/proposition.png" width="800">
    <br>
    <div style="color:orange;
    display: inline-block;
    color: #999; font-size:16px；
    padding: 2px;">
</div>
</center>
---

## How to Integrate Sparsity with Machine Unlearning?
In our paper, we present two innovative strategies for the integration of sparsity with machine unlearning, aiming to augment the efficacy of the unlearning process. 

**Prune first, then unlearn**: Our initial approach involves pruning the model to induce sparsity, employing the One-shot Magnitude Pruning (OMP) technique as detailed by Ma et al. in 2021. Following this, we implement existing machine unlearning methodologies on the now-sparse model. The procedural framework is depicted below:
<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/Sparse_unlearn_neurips23/prune_first.png" width="800">
    <br>
    <div style="color:orange;
    display: inline-block;
    color: #999; font-size:16px；
    padding: 2px;">
    Figure 4: Overview for Prune first, Then Unlearn Strategy.
</div>
</center>

**Sparsity-aware unlearning**: Furthermore, we introduce a novel methodology that does not necessitate pre-existing knowledge of model sparsity. This technique incorporates an $$\ell_1$$ norm-based sparsity penalty directly into the machine unlearning objective function, which leads to the **$$\ell_1$$-sparse MU**:

$$
\theta_u = \underset{\theta}{\text{arg min}} \ L_u(\theta; \theta_o, D_r) + \gamma \|\theta\|_1,
$$

---

## Experimental Results

### Model sparsity improves approximate unlearning. 

In Table 1 below, we explore how model sparsity influences the effectiveness of different machine unlearning (MU) methods within the 'prune first, then unlearn' approach. We compare these methods to the exact unlearning (Retrain) benchmark. We find that increased sparsity consistently enhances unlearning accuracy (UA) and membership inference attack efficacy (MIA-Efficacy), with minimal impact on retained accuracy (RA). As sparsity rises, notably at 95%, the performance gap with Retrain narrows, indicating improved unlearning. Although Retrain experiences a 3% decline in test accuracy (TA) at high sparsity levels, approximate unlearning methods like FT and IU benefit, showing marked improvements in UA and MIA-Efficacy while better maintaining TA.

<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/Sparse_unlearn_neurips23/main_table.png" width="800">
    <br>
    <div style="color:orange;
    display: inline-block;
    color: #999; font-size:16px；
    padding: 2px;">
    Table 1: Performance overview of various MU methods on dense and 95%-sparse models considering different
unlearning scenarios: class-wise forgetting, and random data forgetting.
</div> 
</center>

### Effectiveness of sparsity-aware unlearning.

In Figure 5, we demonstrate the effectiveness of the proposed sparsity-aware unlearning method, i.e., $$\ell_1$$-sparse MU. For clarity, we limit our discussion to comparisons with the FT method and the optimal Retrain strategy, focusing on scenarios of class-wise forgetting and random data forgetting within the CIFAR-10 dataset, using a ResNet-18 model. The results show that $$\ell_1$$-sparse MU surpasses FT in unlearning efficacy, measured by UA and MIA-Efficacy, and effectively reduces the performance gap with Retrain, all while retaining the computational benefits of approximate unlearning. We refer readers to our paper for further exploration of $$\ell_1$$-sparse MU on additional datasets.

<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/Sparse_unlearn_neurips23/l1_sparse.png" width="400">
    <br>
    <div style="color:orange;
    display: inline-block;
    color: #999; font-size:16px；
    padding: 2px;">
    Figure 5: Performance of sparsity-aware unlearning vs. FT and Retrain on class-wise forgetting and random data forgetting under (CIFAR10, ResNet-18)
</div> 
</center>

### Application: MU for Trojan model cleanse.

In our study, we explore machine unlearning (MU) as a defensive technique to mitigate the effects of poisoned data, similar to the approach by Liu et al. We assess the unlearned model using the success rate of backdoor attacks (ASR) and standard accuracy (SA). Figure 6 compares these metrics for the Trojan model and its unlearned counterpart using the FT method across various sparsity levels, and it introduces $$\ell_1$$-sparse MU, showing its cleansing efficacy on a dense model. While the Trojan model's ASR remains high, FT unlearning notably decreases ASR, particularly at 90% sparsity, with minimal impact on SA. Additionally, $$\ell_1$$-sparse MU effectively neutralizes backdoor threats, affirming our unlearning approach as a viable defense against backdoor attacks.

<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/Sparse_unlearn_neurips23/Model_cleanse.png" width="600">
    <br>
    <div style="color:orange;
    display: inline-block;
    color: #999; font-size:16px；
    padding: 2px;">
    Figure 6: Performance of Trojan model cleanse via proposed unlearning vs. model sparsity, where Original refers to the original Trojan model. Left: ASR vs. model sparsity. Right: SA vs. model sparsity.
</div> 
</center>

---


## Acknowledgement

The work of J. Jia, J. Liu, Y. Yao, and S. Liu were supported by the Cisco Research Award and
partially supported by the NSF Grant IIS-2207052, and the ARO Award W911NF2310343. Y. Liu
was partially supported by NSF Grant IIS-2143895 and IIS-2040800.

---

## Citation
```
@article{jia2023model,
  title={Model sparsification can simplify machine unlearning},
  author={Jia, Jinghan and Liu, Jiancheng and Ram, Parikshit and Yao, Yuguang and Liu, Gaowen and Liu, Yang and Sharma, Pranay and Liu, Sijia},
  journal={arXiv preprint arXiv:2304.04934},
  year={2023}
}
```

---

## References

[1] Cao, Yinzhi, and Junfeng Yang. "Towards making systems forget with machine unlearning." 2015 IEEE symposium on security and privacy. IEEE, 2015.

[2] Thudi, Anvith, et al. "Unrolling sgd: Understanding factors influencing machine unlearning." 2022 IEEE 7th European Symposium on Security and Privacy (EuroS&P). IEEE, 2022.