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
other_message: "<b>WARNING: This page contains model outputs that may be offensive in nature. </b>"
video: "https://www.youtube.com/watch?v=O_K0wETC6jg"
buttons:
    - text: "Code"
      url: "https://github.com/OPTML-Group/Unlearn-Saliency"
    - text: "Paper"
      url: "https://arxiv.org/pdf/2310.12508.pdf"
    - text: "Video"
      url: "https://ieeexplore.ieee.org/document/9152147"
    - text: "BibTeX"
      url: "https://scholar.googleusercontent.com/scholar.bib?q=info:AAbyvk63DNkJ:scholar.google.com/&output=citation&scisdr=ClH0TJIHELP_ktx_0sk:AFWwaeYAAAAAZjF6ysmH10FESS37-Ys4KZYSHAw&scisig=AFWwaeYAAAAAZjF6ymst44nddxHAz_Rg0MCfHgQ&scisf=4&ct=citation&cd=-1&hl=en"
---

<center>
    <iframe width="800" height="450" src="https://www.youtube.com/embed/O_K0wETC6jg?si=UHfAPfjJ5EzonC8l" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</center>


## Abstract
With evolving data regulations, machine unlearning (MU) has become an important tool for fostering trust and safety in today's AI models. However, existing MU methods focusing on data and/or weight perspectives often suffer limitations in unlearning accuracy, stability, and cross-domain applicability. To address these challenges, we introduce the concept of 'weight saliency' for MU, drawing parallels with input saliency in model explanation. This innovation directs MU's attention toward specific model weights rather than the entire model, improving effectiveness and efficiency. The resultant method that we call saliency unlearning (SalUn) narrows the performance gap with 'exact' unlearning (model retraining from scratch after removing the forgetting data points). To the best of our knowledge, SalUn is the first principled MU approach that can effectively erase the influence of forgetting data, classes, or concepts in both image classification and generation tasks. As highlighted below, For example, SalUn yields a stability advantage in high-variance random data forgetting, *e.g.*, with a 0.2% gap compared to exact unlearning on the CIFAR-10 dataset. Moreover, in preventing conditional diffusion models from generating harmful images, SalUn achieves nearly 100% unlearning accuracy, outperforming current state-of-the-art baselines like Erased Stable Diffusion and Forget-Me-Not.

<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/salun_iclr24/transition_new.gif" width="800">
    <br>
    <div style="color:orange;
    display: inline-block;
    color: #999; font-size:16px；
    padding: 2px;">
    Figure 1. Example comparison of pre/after unlearning by SalUn. 
    <br> (Left) Concept "Nudity"; (Middle) Object "Dog"; (Right) Style "Sketch". </div>
</center>


## Algorithms: Saliency Unlearning (SalUn)
We incorporates weight saliency into the unlearning process. Weight saliency is used to identify model weights contributing the most to the model output. Here, we utilize the weight saliency to identify the weights that are sensitive to the forgetting ***data/class/concept*** with the gradient of a forgetting loss (denoted as $$\ell_{\mathrm{f}}(\boldsymbol{\theta}; \mathcal{D}_\mathrm{f})$$) with respect to the model weights variable $$\boldsymbol{\theta}$$ under the forgetting dataset $$\mathcal{D}_\mathrm{f}$$. By applying a hard thresholding operation, we can then obtain the desired weight saliency map<sup>[\[1\]](#refer-anchor-1)</sup>:

$$
    \mathbf m_{\mathrm{S}}   = \mathbf 1 \left ( \left |  \nabla_{\boldsymbol{\theta}} \ell_{\mathrm{f}} (\boldsymbol{\theta}; \mathcal{D}_\mathrm{f}) \left . \right |_{\boldsymbol{\theta} = \boldsymbol{\theta}_{\mathrm{o}} } \right  | \geq  \gamma \right )
$$


 where $$ \mathbf 1 (\mathbf g \geq \gamma ) $$ is an element-wise indicator function which yields a value of $$ 1 $$ for the $$i$$-th element if $$ g_i \geq \gamma $$ and $$ 0 $$ otherwise, and $$ \gamma > 0 $$ is a hard threshold. We express the unlearning model $$ \boldsymbol{\theta_\mathrm{u}} $$ as


$$
    \boldsymbol{\theta}_\mathrm{u} = \underbrace{\mathbf m_{\mathrm{S}} \odot (\Delta \boldsymbol{\theta} + \boldsymbol{\theta_{\mathrm{o}}})}_\text{salient weights} + \underbrace{ (\mathbf 1 - \mathbf m_{\mathrm{S}}) \odot \boldsymbol{\theta_{\mathrm{o}}}}_\text{original weights}
$$

<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/salun_iclr24/teaser-v2.png" width="800">
    <br>
    <div style="color:orange;
    display: inline-block;
    color: #999; font-size:16px；
    padding: 2px;">
    Figure 2. Schematic overview of comparing conventional unlearning methods with our proposal (SalUn) in the context of mitigating the influence of the harmful concept of ‘nudity’ in DM. </div>
</center>

The resultant method that we call ***Saliency Unlearning (SalUn)***. One  advantage of SalUn is its plug-and-play capability, allowing it to be applied on top of existing unlearning methods. In particular, we find that integrating weight saliency with the ***Random Labeling*** method provides a promising MU solution.

In image classification, Random Labeling assigns a random image label to a forgetting data point and then fine-tunes the model on the randomly labeled $$ \mathcal{D}_\mathrm{f} $$. In SalUn, we leverage the idea of Random Labeling to update $$ \boldsymbol{\theta_\mathrm{u}} $$. This gives rise to the following optimization problem associated with SalUn for image classification:

$$
    \min_\mathbf{\theta_\mathrm{u}} ~ L_\text{SalUn}^{(1)} (\boldsymbol{\theta_\mathrm{u}}) \mathrel{\mathop:}=  \mathbb E_{(\mathbf x, y) \sim \mathcal{D}_\mathrm{f}, y^\prime \neq y} \left [ \ell_\mathrm{CE}(\boldsymbol{\theta_\mathrm{u}}; \mathbf x, y^\prime) \right ] + \alpha \mathbb E_{(\mathbf x, y) \sim \mathcal{D}_\mathrm{r}} \left [ \ell_\mathrm{CE}(\boldsymbol{\theta_\mathrm{u}}; \mathbf x, y) \right ] 
$$

where $$ y^\prime $$ is the random label of the image $$ \mathbf x $$ different from $$y$$. Additionally, to achieve a balance between unlearning on forgetting data points and preserving the model's generalization ability for non-forgetting data points,  the regularization term on $$\mathcal{D}_\mathrm r$$ preserved, with $$\alpha > 0$$ as a regularization parameter.

Furthermore, we extend the use of Radom Labeling to the image generation context within SalUn. In this context, Radom Labeling is implemented by associating the image of the forgetting concept with a misaligned concept. To maintain the image-generation capability of the DM, we also introduce the MSE loss  on the remaining dataset $$ \mathcal{D}_\mathrm{r} $$ as a regularization. This leads to  the   optimization problem of SalUn for image generation:

$$
    \min_\mathbf{\theta_\mathrm{u}} ~  L_\text{SalUn}^{(2)} (\boldsymbol{\theta}_\mathrm{u}) \mathrel{\mathop:}=  \mathbb{E}_{(\mathbf x, c) \sim \mathcal D_\mathrm{f}, t, \epsilon \sim \mathcal{N}(0,1), c^\prime \neq c  } \left [ \| \epsilon_\mathbf{\theta_\mathrm{u}}(\mathbf x_t | c^\prime) - \epsilon_\mathbf{\theta_\mathrm{u}}(\mathbf x_t | c) \|_2^2 \right ] + \beta \ell_\mathrm{MSE}(\boldsymbol{\theta_\mathrm{u}}; \mathcal D_\mathrm{r})
$$

where $$ c^\prime \neq c $$ indicates that the concept $$ c^\prime $$ is different from $$ c $$, $$ \boldsymbol{\theta_\mathrm{u}} $$ is the saliency-based unlearned model, $$ \beta > 0 $$ is a regularization parameter to place an optimization tradeoff between the RL-based unlearning  loss over the forgetting dataset $$ \mathcal D_\mathrm{f} $$ and the diffusion training loss $$ \ell_\mathrm{MSE}(\boldsymbol{\theta_\mathrm{u}}; \mathcal D_\mathrm{r})$$ on the non-forgetting dataset $$ \mathcal{D}_\mathrm{r} $$ (to preserve image generation quality).


## Experiment results highlight

* **Data-wise forgetting in image classification**
<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/salun_iclr24/tab1.png" width="800">
    <br>
    <div style="color:orange;
    display: inline-block;
    color: #999; font-size:16px；
    padding: 2px;">
    Table 1. Performance summary of various MU methods for image classification (including the proposed SalUn and SalUn-soft and 7 other baselines) in two unlearning scenarios, 10% random data forgetting and 50% random data forgetting, on CIFAR-10 using ResNet-18. The result format is given by a<sub>±b</sub> with mean a and standard deviation b over 10 independent trials. A performance gap against Retrain is provided in (<span style="color:blue">•</span>).   
    </div>
</center>
<br>

* **Object-wise forgetting in image generation**
<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/salun_iclr24/church.jpg" width="800">
    <br>
        <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/salun_iclr24/chain_saw.jpg" width="800">
    <br>
    <div style="color:orange;
    display: inline-block;
    color: #999; font-size:16px；
    padding: 2px;">
    Figure 3. Example comparison on Imgaenette of pre/after object-wise forgetting by SalUn.
    </div>
</center>
<br>

<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/salun_iclr24/dog.jpg" width="800">
    <br>
        <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/salun_iclr24/cat.jpg" width="800">
    <br>
    <div style="color:orange;
    display: inline-block;
    color: #999; font-size:16px；
    padding: 2px;">
    Figure 4. Example comparison on Unlearn Canvas of pre/after object-wise forgetting by SalUn.
    </div>
</center>
<br>

* **Concept-wise forgetting in image generation**
<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/salun_iclr24/nudity_1.jpg" width="800">
    <br>
        <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/salun_iclr24/nudity_2.jpg" width="800">
    <br>
    <div style="color:orange;
    display: inline-block;
    color: #999; font-size:16px；
    padding: 2px;">
    Figure 5. Example comparison on I2P of pre/after concept-wise forgetting by SalUn.
    </div>
</center>
<br>

* **Style-wise forgetting in image generation**
<center>
    <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/salun_iclr24/van_gogh.jpg" width="800">
    <br>
        <img style="border-radius: 0.3125em;
    box-shadow: 0 2px 4px 0 rgba(34,36,38,.12),0 2px 10px 0 rgba(34,36,38,.08);" 
    src="{{ site.url }}{{ site.baseurl }}/images/postpic/salun_iclr24/bricks.jpg" width="800">
    <br>
    <div style="color:orange;
    display: inline-block;
    color: #999; font-size:16px；
    padding: 2px;">
    Figure 6. Example comparison on Unlearn Canvas of pre/after style-wise forgetting by SalUn.
    </div>
</center>

### Acknowledgement

C. Fan, J. Liu, Y. Zhang and S. Liu were supported by the Cisco Research Faculty Award and the National Science Foundation (NSF) Robust Intelligence (RI) Core Program Award IIS-2207052.


### References
<div id="refer-anchor-1"></div> [1]Samiyuru Menik et al. "Towards modular machine learning solution development: Benefits
and trade-offs" arXiv preprint arXiv:2301.09753, 2023.



### Citation
```
@article{fan2023salun,
  title={Salun: Empowering machine unlearning via gradient-based weight saliency in both image classification and generation},
  author={Fan, Chongyu and Liu, Jiancheng and Zhang, Yihua and Wei, Dennis and Wong, Eric and Liu, Sijia},
  journal={arXiv preprint arXiv:2310.12508},
  year={2023}
}
```