---
layout: paper
title:  "[NeurIPS23 Spotlight] Model Sparsity Can Simplify Machine Unlearning"
date: 2023-12-02 21:00:00
author_list:
  - name: "Jinghan Jia"
    url: "https://jinghanjia.netlify.app"
    affiliation: "1"
    coauthor: true
  - name: "Jiancheng Liu"
    url: "https://ljcc0930.github.io/"
    affiliation: "1"
    coauthor: true
  - name: "Parikshit Ram"
    url: "https://rithram.github.io/"
    affiliation: "2"
  - name: "Yuguang Yao"
    url: "https://www.cse.msu.edu/~yaoyugua/"
    affiliation: "1"
  - name: "Gaowen Liu"
    url: "https://www.linkedin.com/in/gaowen-liu-1b52a610a/"
    affiliation: "3"
  - name: "Yang Liu"
    url: "http://www.yliuu.com/"
    affiliation: "4,5"
  - name: "Pranay Sharma"
    url: "https://sites.google.com/view/pranay-sharma/home"
    affiliation: "6"
  - name: "Sijia Liu"
    url: "https://lsjxjtu.github.io/"
    affiliation: "1,2"
affiliation_list:
  - name: "Michigan State University"
  - name: "IBM Research"
  - name: "Cisco Research"
  - name: "University of California, Santa Cruz"
  - name: "ByteDance Research"
  - name: "Carnegie Mellon University"
buttons:
  - text: "Code"
    url: "https://github.com/OPTML-Group/Unlearn-Sparse"
  - text: "Paper"
    url: "https://arxiv.org/pdf/2304.04934.pdf"
  - text: "Poster"
    url: "https://jinghanjia.netlify.app/assets/img/publication_preview/unlearn-sparse"
maintainer: "<a href='https://jinghanjia.netlify.app'>Jinghan Jia</a>"
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


Machine unlearning (MU) has become essential for complying with data regulations by eliminating the influence of specific data from models. Traditional exact unlearning methods, which involve retraining from scratch, are computationally expensive, prompting the exploration of efficient, approximate alternatives. Our research introduces a model-based approach: sparsity through weight pruning,that narrows the gap between exact and approximate unlearning. We present a new paradigm, "prune first, then unlearn," which integrates a sparsity model into unlearning, and a sparsity-aware technique that further refines approximate unlearning training. Our extensive experiments confirm the effectiveness of our methods, particularly a 77% increase in unlearning efficacy with fine-tuning, and their applicability in mitigating backdoor attacks and improving transfer learning.

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
**Efficicy Challenge**: The ideal MU strategy involves full model retraining, which is inefficient for large models. Therefore, **fast** and **efficient** MU methods are essential. 

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
In our work, we extend the analytical framework of Thudi et al. regarding machine unlearning to encompass sparse models.
 <!-- **Proposition 2** of our paper elucidates that an increase in model sparsity, as indicated by the sparsity pattern $$m$$, contributes to a decrease in the unlearning error. Nonetheless, it is critical to acknowledge that operating within a regime of high sparsity may inversely affect the model’s capacity for generalization. -->
<!-- <center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/Sparse_unlearn_neurips23/proposition.png" width="800">
    <br>
    <div style="color:orange;
    display: inline-block;
    color: #999; font-size:16px；
    padding: 2px;">
</div>
</center> -->

**Theorem:** Given SGD-based training and model pruning mask $$m$$, the unlearning error, $$e(m)$$, characterized by weight distance between an approximate unlearner and the exact unlearner yields

$$ e(m) = \mathcal{O}(\|m \circ (\theta_t - \theta_0)\|_2) $$

where $$\circ$$ is entry-wise product, $$\theta_t$$ is model trained after $$t$$ SGD iterations.This theorem eveals that higher model sparsity, denoted by $$m$$, reduces unlearning error but may compromise generalization at extreme levels.


---

## How to Integrate Sparsity with Machine Unlearning?
In our paper, we present two innovative strategies for the integration of sparsity with machine unlearning, aiming to augment the efficacy of the unlearning process. 

**Prune first, then unlearn**: Our approach starts with pruning via One-shot Magnitude Pruning (OMP) detailed by Ma et al. in 2021. to sparsify the model, then applies machine unlearning methods to this sparse framework. See the process outlined below: 
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

Our paper shows that higher sparsity improves the efficacy of machine unlearning methods in our 'Prune first, then unlearn' paradigm, closely matching the Retrain benchmark, especially at 95% sparsity. Despite a minor TA drop in Retrain at high sparsity, methods like FT and IU display significant gains in unlearning accuracy and attack defense, with less impact on TA.

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

In Fig. 5, we present the efficacy of our $$\ell_1$$-sparse MU method, comparing it with FT and Retrain strategies on CIFAR-10 using ResNet-18. We focus on class-wise and random data forgetting. Results indicate $$\ell_1$$-sparse MU not only outperforms FT in terms of unlearning (measured by UA and MIA-Efficacy) but also narrows the performance gap with Retrain, maintaining computational efficiency. For extended analysis on other datasets, see our paper.


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

Our study examines machine unlearning (MU) for countering poisoned data, using metrics like backdoor attack success rate (ASR) and standard accuracy (SA). Figure 6 shows that our $$\ell_1$$-sparse MU method effectively reduces ASR in the Trojan model, particularly at higher sparsity levels, while maintaining SA, thus proving its efficacy against backdoor threats.

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
@inproceedings{jia2023model,
  title={Model Sparsity Can Simplify Machine Unlearning},
  author={Jia, Jinghan and Liu, Jiancheng and Ram, Parikshit and Yao, Yuguang and Liu, Gaowen and Liu, Yang and Sharma, Pranay and Liu, Sijia},
  booktitle={Thirty-seventh Conference on Neural Information Processing Systems},
  year={2023}
}
```

---

## References

[1] Cao, Yinzhi, and Junfeng Yang. "Towards making systems forget with machine unlearning." 2015 IEEE symposium on security and privacy.

[2] Thudi, Anvith, et al. "Unrolling sgd: Understanding factors influencing machine unlearning." 2022 IEEE 7th European Symposium on Security and Privacy (EuroS&P).

[3] Ma, Xiaolong, et al. "Sanity checks for lottery tickets: Does your winning ticket really win the jackpot?." Advances in Neural Information Processing Systems 34 (2021): 12749-12760.