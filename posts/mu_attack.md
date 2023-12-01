---
layout: paper
title:  "To Generate or Not? Safety-Driven Unlearned Diffusion Models Are Still Easy To Generate Unsafe Images ... For Now"
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

The recent advances in diffusion models (DMs) have revolutionized the generation of complex and diverse images. However, these models also introduce potential safety hazards, such as the production of harmful content and infringement of data copyrights. **Although there have been efforts to create safety-driven unlearning methods to counteract these challenges, doubts remain about their capabilities. To bridge this uncertainty, we propose an evaluation framework built upon adversarial attacks (also referred to as adversarial prompts), in order to discern the trustworthiness of these safety-driven unlearned DMs.** Specifically, our research explores the (worst-case) robustness of unlearned DMs in eradicating unwanted concepts, styles, and objects, assessed by the generation of adversarial prompts. We develop a novel adversarial learning approach called UnlearnDiff that leverages the inherent classification capabilities of DMs to streamline the generation of adversarial prompts, making it as simple for DMs as it is for image classification attacks. This technique streamlines the creation of adversarial prompts, making the process as intuitive for generative modeling as it is for image classification assaults. Through comprehensive benchmarking, we assess the unlearning robustness of five prevalent unlearned DMs across multiple tasks. Our results underscore the effectiveness and efficiency of UnlearnDiff when compared to state-of-the-art adversarial prompting methods.

**(WARNING: This paper contains model outputs that may be offensive in nature.)**

---

## Our Proposal: Evaluation framework for unlearned diffusion models
Our proposed method for generating adversarial prompts, referred to as the ‘Unlearning Diffusion’ attack (UnlearnDiff). **Unlike previous methods for generating adversarial prompts, we leverage the class-discriminative ability of the ‘diffusion classifier’ inherent in a well-trained DM, using it effectively and without additional costs.** This classification perspective within DMs allows us to craft adversarial prompts exclusively with the victim model (i.e., unlearned DM), eliminating the need for an extra auxiliary DM or image classifier. As a result, our proposal streamlines the diffusion costs during the process of generating attacks.

**1. Turning generation into classification: Exploiting DMs' embedded `free' classifier.**

In this work, we will demonstrate that there is no need to introduce an additional DM or classifier because the victim DM inherently serves dual roles  -- image generation and classification.

We next extract the `free classifier` from a DM, referred to as the diffusion classifier [[1](#refer-anchor-1),[2](#refer-anchor-2)]. 
The underlying principle is that classification with a DM can be achieved by applying Bayes rule to the likelihood of model generation $$p_{\boldsymbol \theta}(\mathbf x | c)$$  and the prior probability distribution  $$p(c)$$ over prompts $$\{c_i\}$$ (viewed as image `labels`). $$\mathbf x$$ and $$\boldsymbol \theta$$ represent an image and DM's parameters, respectively. 
According to Bayes' rule, the probability of predicting $$\mathbf x$$ as the `label` $$c$$ is given by

$$
  p_{\boldsymbol \theta}(c_i| \mathbf x) =  \frac{p(c_i) p_{\boldsymbol \theta}(\mathbf x | c_i) }{\sum_j p(c_j) p_{\boldsymbol \theta}(\mathbf x | c_j) }
$$

where $$p(c)$$ can be a uniform distribution, representing a random guess regarding $$\mathbf{x}$$, while $$p_{\boldsymbol \theta}(\mathbf{x} | c_i)$$ is associated with the quality of image generation corresponding to prompt $$c_i$$. In the case of the uniform prior, namely, $$p(c_i) = p(c_j)$$, 
equation (1) can be further simplified to exclusively address the conditional probabilities $$\{p_{\boldsymbol \theta}(\mathbf x | c_i)\}$$. 
In DM, the log-likelihood of $$p_{\boldsymbol \theta}(\mathbf x | c_i)$$  relates to the denoising error, i.e., $$p_{\boldsymbol \theta}(\mathbf x | c_i) \propto \exp \left \{ -\mathbb{E}_{t, \epsilon }[\| \epsilon - \epsilon_{\boldsymbol \theta}(\mathbf x_t | c_i) \|_2^2] \right \}$$, where $$\exp{\cdot}$$ is the exponential function. 
As a result, the diffusion classifier yields

$$
  p_{\boldsymbol \theta}(c_i| \mathbf x) \propto   \frac{  \exp \left \{ -\mathbb{E}_{t, \epsilon}[\| \epsilon - \epsilon_{\boldsymbol \theta}(\mathbf x_t | c_i) \|_2^2] \right \} }{\sum_j  \exp \left \{ -\mathbb{E}_{t, \epsilon }[\| \epsilon - \epsilon_{\boldsymbol \theta}(\mathbf x_t | c_j) \|_2^2] \right \}  }
$$

A key insight is that the DM ($$\boldsymbol \theta$$) can serve as a classifier by evaluating its denoising error for a specific prompt ($c_i$) relative to all the potential errors associated with different prompts.

**2. UnlearnDiff: Diffusion classifier-guided attack against unlearned DMs.**
The task of creating an adversarial prompt ($$c^\prime$$) to evade a victim unlearned DM ($$\boldsymbol \theta^*$$) can be cast as:

$$
  \max_{c^\prime} p_{\boldsymbol \theta^*}(c^\prime | \mathbf x_\mathrm{tgt})
$$

where $$\mathbf{x}_\mathrm{tgt}$$ denotes a target image containing unwanted content (encoded by $$c^\prime$$) which $$\boldsymbol \theta^*$$ intends to forget.
However, there are two challenges when incorporating the classification rule into the attack generation.
First, the objective function requires extensive diffusion-based computations for all prompts and is difficult to optimize in fractional form. The second challenge revolves around determining what prompts, aside from $$c^\prime$$, should be considered to form the classification problem over the `label set` $$\{ c_i \}$$. 

To tackle the above problems, we leverage a key observation in 
 [[2](#refer-anchor-2)]:  Classification only requires the `relative` differences  between the noise errors, rather than their `absolute` magnitudes. Then we can get:
 
$$
  p_{\boldsymbol \theta}(c_i| \mathbf x)   \propto   \frac{ 1 }{\sum_j  \exp \left \{ -\mathbb{E}_{t, \epsilon }[\| \epsilon - \epsilon_{\boldsymbol \theta}(\mathbf x_t | c_j) \|_2^2] \right \} / \exp \left \{ -\mathbb{E}_{t, \epsilon }[\| \epsilon - \epsilon_{\boldsymbol \theta}(\mathbf x_t | c_i) \|_2^2] \right \}  } \nonumber 
$$

$$
  = \frac{ 1 }{\sum_j  \exp \left \{ \mathbb{E}_{t, \epsilon }[\| \epsilon - \epsilon_{\boldsymbol \theta}(\mathbf x_t | c_i) \|_2^2] -\mathbb{E}_{t, \epsilon }[\| \epsilon - \epsilon_{\boldsymbol \theta}(\mathbf x_t | c_j) \|_2^2] \right \}    }
$$

If we view the adversarial prompt $$c^\prime$$ as the targeted prediction (i.e., $$c_i = c^\prime$$), then we can solve the attack generation problem by

$$
  \min_{c^\prime}  \sum_j  \exp \left \{ \mathbb{E}_{t, \epsilon }[\| \epsilon - \epsilon_{\boldsymbol \theta^*}(\mathbf x_{\mathrm{tgt},t} | c^\prime) \|_2^2] -\mathbb{E}_{t, \epsilon }[\| \epsilon - \epsilon_{\boldsymbol \theta^*}(\mathbf x_{\mathrm{tgt},t} | c_j) \|_2^2]
  \right \}
$$

where $$\mathbf x_{\mathrm{tgt},t}$$ represents the noisy image at diffusion time step $$t$$ corresponding to the original noiseless image $$\mathbf{x}_{\mathrm{tgt}}$$. 
Moreover, given that $$\exp$$ is a convex function, the individual objective function (for a given $$j$$) is upper bounded by:

$$
 \exp \left \{ \mathbb{E}_{t, \epsilon }[\| \epsilon - \epsilon_{\boldsymbol \theta^*}(\mathbf x_{\mathrm{tgt},t} | c^\prime) \|_2^2]  \right \} + \underbrace{ \exp \left \{ -\mathbb{E}_{t, \epsilon }[\| \epsilon - \epsilon_{\boldsymbol \theta^*}(\mathbf x_{\mathrm{tgt},t} | c_j) \|_2^2]
          \right \} }_\text{independent of attack variable $c^\prime$}
$$

where the second term is \textit{not} a function of the optimization variable $$c^\prime$$, irrespective of our choice of another prompt $$c_j$$ (corresponding to a class  unrelated to $$c$$).

Then, we arrive at the following simplified optimization problem for attack generation:

$$
  \min_{c^\prime} \mathbb{E}_{t, \epsilon }[\| \epsilon - \epsilon_{\boldsymbol \theta^*}(\mathbf x_{\mathrm{tgt},t} | c^\prime) \|_2^2]
$$

where we excluded $$\exp$$ as it is monotonically increasing with respect to its input argument. 

---
## Remarks

**Remark 1**

A key takeaway is that we can optimize the adversarial prompt $$c^\prime$$ by aligning it with the diffusion training objective    \eqref{eq: diffusion_training}, given the victim model $$\boldsymbol \theta^*$$ and the target image $$\mathbf{x}_\mathrm{tgt}$$ (to which the forward noise-injection process is applied, rather than the latent embedding $$\mathbf z_t$$).

Additionally, in contrast to existing adversarial prompt generation methods for DMs, our proposed adversarial attack does `not` depend on an auxiliary DM or an external image classifier. To underscore this advantage, let's examine an attack formulation employed in the concurrent work `P4D`:

$$
  \min_{c^\prime} \mathbb{E}_{t, \epsilon }[\| \epsilon_{\btheta} (\mathbf z_t | c) - \epsilon_{\boldsymbol \theta^*}(\mathbf z_t | c^\prime) \|_2^2]
$$

where $$\boldsymbol \theta$$ represents the original DM without unlearning, $$\mathbf{z}_t$$ is the latent embedding for image generation, and $$c$$ is an `inappropriate` prompt intended to generate a `harmful` image. 

It is clear that the former necessitates an extra diffusion process (represented by $$\boldsymbol \theta$$) to generate an unwanted image when provided with a prompt $$c$$ (the unlearning target). This introduces a large computational overhead during optimization. In contrast, the selection of $$\mathbf x_\mathrm{tgt}$$ can be performed offline and from diverse image sources.


**Remark 2**

The derivation is contingent upon the upper bounding of the individual relative difference concerning $$c_j$$ in \eqref{eq: upper_bound}. Nonetheless, this relaxation retains its tightness if we frame the task of predicting $$c^\prime$$ as a `binary` classification problem. In this scenario, we can interpret $$c_j$$ as the  non-$$c^\prime$$ class (e.g., non-Van Gogh painting style vs. $$c^\prime$$ containing Van Gogh style, which is the concept to be erased). 


**Remark 3**

As the adversarial perturbations to be optimized are situated in the discrete text space, we employ projected gradient descent (PGD) to solve the optimization problem. Yet, it is worth noting that different from vanilla PGD for continuous optimization, the projection operation is defined within the discrete space. It serves to map the token embedding to discrete texts, following a similar approach utilized in  [[3](#refer-anchor-3)] for generating natural language processing (NLP) attacks.

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
@article{zhang2023generate,
  title={To Generate or Not? Safety-Driven Unlearned Diffusion Models Are Still Easy To Generate Unsafe Images... For Now},
  author={Zhang, Yimeng and Jia, Jinghan and Chen, Xin and Chen, Aochuan and Zhang, Yihua and Liu, Jiancheng and Ding, Ke and Liu, Sijia},
  journal={arXiv preprint arXiv:2310.11868},
  year={2023}
}
```

---

## References

<div id="refer-anchor-1"></div>  [1] Chen, Huanran, et al. (2023) "Robust Classification via a Single Diffusion Model."

<div id="refer-anchor-2"></div>  [2] Li, Alexander C., et al. (2023) "Your diffusion model is secretly a zero-shot classifier."

<div id="refer-anchor-3"></div> [3] Hou, Bairu, et al. (2022) "Textgrad: Advancing robustness evaluation in nlp by gradient-driven optimization.".