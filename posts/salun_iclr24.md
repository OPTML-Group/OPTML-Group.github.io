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
    Figure 1. Schematic overview of comparing conventional unlearning methods with our proposal (SalUn) in the context of mitigating the influence of the harmful concept of ‘nudity’ in DM. </div>
</center>

## Abstract
With evolving data regulations, machine unlearning (MU) has become an important tool for fostering trust and safety in today's AI models. However, existing MU methods focusing on data and/or weight perspectives often suffer limitations in unlearning accuracy, stability, and cross-domain applicability. To address these challenges, we introduce the concept of 'weight saliency' for MU, drawing parallels with input saliency in model explanation. This innovation directs MU's attention toward specific model weights rather than the entire model, improving effectiveness and efficiency. The resultant method that we call saliency unlearning (SalUn) narrows the performance gap with 'exact' unlearning (model retraining from scratch after removing the forgetting data points). To the best of our knowledge, SalUn is the first principled MU approach that can effectively erase the influence of forgetting data, classes, or concepts in both image classification and generation tasks. As highlighted below, For example, SalUn yields a stability advantage in high-variance random data forgetting, *e.g.*, with a 0.2% gap compared to exact unlearning on the CIFAR-10 dataset. Moreover, in preventing conditional diffusion models from generating harmful images, SalUn achieves nearly 100% unlearning accuracy, outperforming current state-of-the-art baselines like Erased Stable Diffusion and Forget-Me-Not.

**WARNING**: This paper contains model outputs that may be offensive in nature.


## What is Machine Unlearning(MU)?

* Eliminate undesirable data influence (e.g., sensitive or illegal information) and associated model capabilities, while maintaining utility. 
* Applications: Removing sensitive data information, copyright protection, harmful content degeneration, etc.


## How to Evaluate MU’s Performance?
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/images/postpic/salun_iclr24/fig0.jpg" title="mu" class="img-fluid" zoomable=true %}
    </div>
</div>


## Limitations of Current MU Methods

**Lack of Stability to forgetting data amount**  
Fig.2 (a) shows sensitivity of unlearning accuracy gaps with respect to Retrain (measured by ‘|Method − Retrain|’) as a function of forgetting data amount. Five existing MU methods (FT, RL, GA, IU, ℓ1-sparse) are included. As we can see, the unlearning effectiveness of existing MU methods observed at a 10% forgetting data quantity does not necessarily hold when the forgetting data quantity is increased to 50%.  

**Lack of Stability to choice of hyperparameters**  
We use IU (influence unlearning) as an example, where the tuning of the Fisher information regularization parameter is necessay. Fig.2 (b) illustrates the variances of unlearning accuracies using Retrain, IU, and the proposed weight saliency-integrated IU across various hyperparameter choices. The box size represents the variance of UA values across hyperparameter values. The integration with our proposal (SalUn) reduces this instability.
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/images/postpic/salun_iclr24/fig1.jpg" title="stability" class="img-fluid" zoomable=true %}
    </div>
</div>
<div class="caption" style="color: #999; font-size:16px; padding: 2px;">
    Figure 2. Demonstration of the instability limitations of MU methods on CIFAR-10.
</div>

**Lack of Generality for different tasks**  
MU methods for image classification can not be adapted to image generation. In Fig 3, we exam five existing MU methods: Retrain, GA, RL, FT and ℓ1-sparse. Existing MU methods tend to either over-forget, resulting in poor generation quality for image classes in Df (e.g., GA, RL), or under-forget, leading to unsuccessful unlearning with regard to ‘airplane’ images (e.g., FT, ℓ1-sparse). This stands in sharp contrast to Retrain.
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/images/postpic/salun_iclr24/fig2.jpg" title="generality" class="img-fluid" zoomable=true %}
    </div>
</div>
<div class="caption" style="color: #999; font-size:16px; padding: 2px;">
    Figure 3. Performance of MU baselines on DMs illustrated using DDPM with classifier-free guidance on CIFAR-10. Each column contains 4 images, generated from the same noise seed over 1000 time steps for the forgetting class ‘airplane’ and non-forgetting classes (‘car’, ‘bird’, ‘horse’, and ‘truck’).  
</div>


## Weight Saliency
Weight saliency is used to identify model weights contributing the most to the model output. Here, we utilize the weight saliency to identify the weights that are sensitive to the forgetting **data/class/concept** with the gradient of a forgetting loss (denoted as $$\ell_{\mathrm{f}}(\boldsymbol{\theta}; \mathcal{D}_\mathrm{f})$$) with respect to the model weights variable $$\boldsymbol{\theta}$$ under the forgetting dataset $$\mathcal{D}_\mathrm{f}$$. By applying a hard thresholding operation, we can then obtain the desired weight saliency map<sup>[\[1\]](#refer-anchor-1)</sup>:

$$
    \mathbf m_{\mathrm{S}}   = \mathbf 1 \left ( \left |  \nabla_{\boldsymbol{\theta}} \ell_{\mathrm{f}} (\boldsymbol{\theta}; \mathcal{D}_\mathrm{f}) \left . \right |_{\boldsymbol{\theta} = \boldsymbol{\theta}_{\mathrm{o}} } \right  | \geq  \gamma \right )
$$


 where $$ \mathbf 1 (\mathbf g \geq \gamma ) $$ is an element-wise indicator function which yields a value of $$ 1 $$ for the $$i$$-th element if $$ g_i \geq \gamma $$ and $$ 0 $$ otherwise, and $$ \gamma > 0 $$ is a hard threshold. We express the unlearning model $$ \boldsymbol{\theta_\mathrm{u}} $$ as


$$
    \boldsymbol{\theta}_\mathrm{u} = \underbrace{\mathbf m_{\mathrm{S}} \odot \boldsymbol{\theta}}_\text{salient weights} + \underbrace{ (\mathbf 1 - \mathbf m_{\mathrm{S}}) \odot \boldsymbol{\theta_{\mathrm{o}}}}_\text{original weights}
$$


We find that the forgetting loss in Gradient Ascent presents a unified, effective, and simple solution in image classification and generation. This is given by the training loss over the forgetting dataset $$ \mathcal{D}_\mathrm{f}$$:


$$
     \text{Classification: } \ell_\mathrm{f} (\boldsymbol{\theta} ; \mathcal D_\mathrm{f}) = \mathbb E_{(\mathbf x, y) \sim \mathcal D_\mathrm{f}} [ \ell_{\mathrm{CE}}(\boldsymbol{\theta}; \mathbf x ,y)]
$$


$$
     \text{Generation: } \ell_\mathrm{f} (\boldsymbol{\theta} ; \mathcal D_\mathrm{f}) =  \mathbb{E}_{t, \epsilon \sim \mathcal{N}(0,1)}[\| \epsilon - \epsilon_{\boldsymbol \theta}(\mathbf x_t | c_\mathrm{f}) \|_2^2]
$$


## Saliency-based unlearning (SalUn)

We introduce SalUn, which incorporates the saliency-aware unlearning variables $$ \boldsymbol{\theta_\mathrm{u}} $$  into the unlearning process.
One  advantage of SalUn is its plug-and-play capability, allowing it to be applied on top of existing unlearning methods. 
In particular, we find that integrating weight saliency with the Random Labeling method provides a promising MU solution.

In image classification, Random Labeling assigns a random image label to a forgetting data point and then fine-tunes the model on the randomly labeled $$ \mathcal{D}_\mathrm{f} $$. In SalUn, we leverage the idea of Random Labeling to update $$ \boldsymbol{\theta_\mathrm{u}} $$. This gives rise to the following optimization problem associated with SalUn for image classification:

$$
    \min_\mathbf{\theta_\mathrm{u}} ~ L_\text{SalUn}^{(1)} (\boldsymbol{\theta_\mathrm{u}}) \mathrel{\mathop:}=  \mathbb E_{(\mathbf x, y) \sim \mathcal{D}_\mathrm{f}, y^\prime \neq y} \left [ \ell_\mathrm{CE}(\boldsymbol{\theta_\mathrm{u}}; \mathbf x, y^\prime) \right ]
$$

where $$ y^\prime $$ is the random label of the image $$ \mathbf x $$ different from $$y$$. Additionally, to achieve a balance between unlearning on forgetting data points and preserving the model's generalization ability for non-forgetting data points, we usually fine-tune the original model $$ \boldsymbol{\theta_\mathrm{o}} $$ for a small number of epochs, e.g., 10 epochs in the classification task.

Furthermore, we extend the use of Radom Labeling to the image generation context within SalUn. In this context, Radom Labeling is implemented by associating the image of the forgetting concept with a misaligned concept. To maintain the image-generation capability of the DM, we also introduce the MSE loss  on the remaining dataset $$ \mathcal{D}_\mathrm{r} $$ as a regularization. This leads to  the   optimization problem of SalUn for image generation:

$$
    \min_\mathbf{\theta_\mathrm{u}} ~  L_\text{SalUn}^{(2)} (\boldsymbol{\theta}_\mathrm{u}) \mathrel{\mathop:}=  \mathbb{E}_{(\mathbf x, c) \sim \mathcal D_\mathrm{f}, t, \epsilon \sim \mathcal{N}(0,1), c^\prime \neq c  } \left [ \| \epsilon_\mathbf{\theta_\mathrm{u}}(\mathbf x_t | c^\prime) - \epsilon_\mathbf{\theta_\mathrm{u}}(\mathbf x_t | c) \|_2^2 \right ] + \alpha \ell_\mathrm{MSE}(\boldsymbol{\theta_\mathrm{u}}; \mathcal D_\mathrm{r})
$$

where $$ c^\prime \neq c $$ indicates that the concept $$ c^\prime $$ is different from $$ c $$, $$ \boldsymbol{\theta_\mathrm{u}} $$ is the saliency-based unlearned model, $$ \alpha > 0 $$ is a regularization parameter to place an optimization tradeoff between the RL-based unlearning  loss over the forgetting dataset $$ \mathcal D_\mathrm{f} $$ and the diffusion training loss $$ \ell_\mathrm{MSE}(\boldsymbol{\theta_\mathrm{u}}; \mathcal D_\mathrm{r})$$ on the non-forgetting dataset $$ \mathcal{D}_\mathrm{r} $$ (to preserve image generation quality).


## Experiment results highlight

* **Data-wise forgetting in image classification**
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/images/postpic/salun_iclr24/tab1.jpg" title="overview of salun" class="img-fluid" zoomable=true %}
    </div>
</div>
<div class="caption" style="color: #999; font-size:16px; padding: 2px;">
    Table 1. Performance summary of various MU methods for image classification (including the proposed SalUn and SalUn-soft and 7 other baselines) in two unlearning scenarios, 10% random data forgetting and 50% random data forgetting, on CIFAR-10 using ResNet-18. The result format is given by a<sub>±b</sub> with mean a and standard deviation b over 10 independent trials. A performance gap against Retrain is provided in (<span style="color:blue">•</span>). 
</div>

* **Concept-wise forgetting in image generation**
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/images/postpic/salun_iclr24/fig3.jpg" title="overview of salun" class="img-fluid" zoomable=true %}
    </div>
</div>
<div class="caption" style="color: #999; font-size:16px; padding: 2px;">
    Figure 4. Eliminate the NSFW (not safe for work) concepts, inappropriate image prompts (I2P). Examples of generated images using SDs w/ and w/o MU. The unlearning methods include ESD, FMN, and SalUn (ours). Each column represents generated images using different SDs with the same prompt(denoted by P<sub>i</sub>) and the same seed.
</div>

* **Class-wise forgetting in image generation**
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/images/postpic/salun_iclr24/fig4.jpg" title="overview of salun" class="img-fluid" zoomable=true %}
    </div>
</div>
<div class="caption" style="color: #999; font-size:16px; padding: 2px;">
    Figure 5. Examples of generated images using SalUn. From the rows below, diagonal images represent the forgetting class, while non-diagonal images represent the remaining class.
</div>


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