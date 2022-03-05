---
title: "OTML - Research"
layout: textlay
excerpt: "OTML -- Research"
sitemap: false
permalink: /research/
---


# Research

As AI moves from the lab into the real world (e.g., autonomous vehicles), ensuring its safety becomes a paramount requirement prior to its deployment. Moreover, as datasets, ML/DL models, and learning tasks become increasingly complex, getting ML/DL to scale calls for new advances in learning algorithm design. More broadly, the study towards robust and scalable AI could make a significant impact on machine learning theories, and induce more promising applications in, e.g., automated ML, meta-learning, privacy and security, hardware design, and big data analysis. We seek a new learning frontier when the current learning algorithms become infeasible, and formalize foundations of secure learning.


Here are some directions and techniques that we currently work on:

**Adversarial Robustness of Deep Neural Networks** ![]({{ site.url }}{{ site.baseurl }}/images/respic/adv_shirt.png){: style="width: 250px; float: right; margin: 0px 10px"}It has been widely known that deep neural networks (DNNs) are vulnerable to adversarial attacks that appear not only in the digital world but also in the physical world. Along this direction, we highlight two of our achievements.

* First, our ECCV’20 work designed 'Adversarial T-shirt’ ([paper](https://arxiv.org/pdf/1910.11099.pdf), [demo](https://drive.google.com/file/d/1S9P56hdnQWC_Rffj1VQsHF-FcazQs2Xy/view?usp=sharing), over 200 media coverage on the web), a robust physical adversarial example for evading person detectors even if it could undergo non-rigid deformation due to a moving person’s pose changes. We have shown that the adversarial T-shirt achieves 74% and 57% attack success rates in the digital and physical worlds respectively against YOLOv2. In contrast, the state-of-the-art physical attack method to fool a person detector only achieves 18% attack success rate.

* Second, our ICLR’21 work ([paper](https://openreview.net/pdf?id=PH5PH9ZO_4), [code](https://github.com/ALFA-group/adversarial-code-generation), [MIT-News](https://news.mit.edu/2021/toward-deep-learning-models-that-can-reason-about-code-like-humans-0415)) designed ‘Adversarial Program’, a method for finding and fixing weaknesses in automated programming tools. We have found that code-processing models can be deceived simply by renaming a variable, inserting a bogus print statement, or introducing other cosmetic operations into programs the model tries to process. These subtly altered programs function normally, but dupe the model into processing them incorrectly, rendering the wrong decision. We show that our best attack proposal achieves a 52% improvement over a state-of-the-art attack generation approach for programs trained on a SEQ2SEQ model. We also show that the proposed adversarial programs can be further exploited to train a program languaging model robust against prediction-evasion attacks.

**Zeroth-Order (ZO) Optimization: Theory, Methods and Applications.** 
![]({{ site.url }}{{ site.baseurl }}/images/respic/ZO.png){: style="width: 250px; float: left; margin: 0px  10px"}
ZO optimization (learning without gradients) is increasingly embraced for solving many machine learning (ML) problems, where explicit expressions of the gradients are difficult or infeasible to obtain. Appealing applications include, e.g., robustness evaluation of black-box deep neural networks (DNNs), hyper-parameter optimization for automated ML, meta-learning, DNN diagnosis and explanation, and scientific discovery using black-box simulators. An illustrative example of ZO optimization versus first-order optimization is shown below.(see [Tutorial](https://ieeexplore.ieee.org/document/9186148) work on IEEE Signal Processing Magazine)

<!-- **Nanofabricated "Smart Tips"**.
![]({{ site.url }}{{ site.baseurl }}/images/respic/SmartTip.png){: style="width: 250px; float: left; margin: 0px  10px"}
One of the  projects back from my job-proposal is to develop nanofabricated STM tips. The idea behind these “smart tips” is to use the technologies that were developed over decades in nanofabrication and make them available for scanning probe by using a nano-device instead of the traditional STM tungsten tip. One gains the flexibility of using different functionalities that are known from the fields of nanofabrication and mesoscopic physics. We are collaborating with the group Simon Groeblacher at TU Delft to realize this concept, benefitting from their unparalleled micro/nano fabrication know how.  A prototype of a smart tip is shown to the left. See publications in Microsyst Nanoeng, Nanotechnology, and PRB. -->

<!-- **Josephson STM.** Josephson STM has the ability to gain insight into spatial variations of the order parameter, or superfluid density. We have managed to, for the first time, use JSTM with atomic resolution on a quantum material.
We have used atomic-resolution Josephson scanning tunneling microscopy to reveal a strongly inhomogeneous superfluid in the iron-based superconductor FeTe0.55Se0.45. The results and their implications are published in Nature.

We also detected and investigated a quite particular YSR state in the same material. -->

**Ultra-stable SI-STM instrument.**  ![]({{ site.url }}{{ site.baseurl }}/images/respic/STMHead.png){: style="width: 250px; float: right; margin: 0px 10px"}
For SI-STM, having the most stable STM head is key. We have used finite element simulations, good choices in material science, and craftsmanship to build the most stable STM head in the world, to our knowledge. See publication in RSI.


**Strange Metals.** The strange metal phase might be the most mysterious phase of high-temperature superconductors. Here, the electrical resistivity grows linearly with temperature T in large areas of the phase diagram, with a mean free path that diminishes to a fraction of the interatomic distance. T-linear resistivity is often associated with quantum critical points and marginal-Fermi-liquid physics. In strange metals, the mystery seems to go even further: we deal with something that looks like a quantum critical phase over an extended range of the phase diagram instead of cumulating in a point. There exists no consistent theory for strange metals, leading to more adventurous new approaches including the holographic theories that use insights from gravity to explain strange metals (a recent textbook on this was written by our colleagues at Leiden University, Schalm and Zaanen).
We are part of the 'Strange Metal consortium NL' that includes the groups of Hussey, Golden, van Heumen, Zaanen, Schalm, Stoof and Vandoren. 

**Magnetic fluctuations and electron spin resonance.**
![]({{ site.url }}{{ site.baseurl }}/images/respic/SpinFluc.png){: style="width: 70%; float: center; margin: 10px"}

**Twisted bilayer graphene and other material with super-periodicities.**
We have proposed that artificial super-periodicities can lead to improved superconductivity, both because of increased density of states and because of phase space arguments (see image from our SciPost publication below). Perhaps for different reasons, twisted bilayer graphene has been shown to superconduct! We are investigate this material with the groups of Efetov, Baumberger, and van der Molen.

![]({{ site.url }}{{ site.baseurl }}/images/respic/SciPost.png){: style="width: 70%; float: center; margin: 0px"}

### ... and more.
