---
title: "OPTML - Home"
layout: homelay
# excerpt: "OPTML Group at Michigan State University."
sitemap: false
permalink: /
---

### About Us
 


<style>
.about-wrap{
  display: flex;
  align-items: flex-start;
  gap: 16px;
}


.about-wrap .about-text{
  flex: 1;
  min-width: 0;  
}


.about-wrap .about-photo-link{
  flex: 0 0 auto;
  margin-left: auto;     
  display: inline-block; 
  line-height: 0;        
}


.about-wrap img.about-photo{
  display: block;
  width: 145px;          
  height: auto;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0,0,0,.08);
  transition: transform 0.25s ease, box-shadow 0.25s ease;
  cursor: pointer;
}

.about-wrap img.about-photo:hover{
  transform: scale(1.05); /* 悬停时放大 5% */
  box-shadow: 0 4px 16px rgba(0,0,0,.15);
}

/* 移动端：上下排 */
@media (max-width: 768px){
  .about-wrap{
    flex-direction: column;
    align-items: center;
  }
  .about-wrap .about-photo-link{
    margin-left: 0;
  }
  .about-wrap img.about-photo{
    width: 100%;
    max-width: 480px;
  }
}
</style>

<div class="about-wrap" markdown="0">
  <div class="about-text" markdown="1">
  **OP**timization and **T**rustworthy **M**achine **L**earning (OPTML) group is an active research group at
  [Michigan State University](https://www.msu.edu). Our research interests span the areas of machine learning (ML)/ deep learning (DL), optimization, computer vision, security, signal processing and data science, with a focus on developing learning algorithms and theory, as well as robust and explainable artificial intelligence (AI). These research themes provide a solid foundation for reaching the long-term research objective: __Making AI systems scalable and trustworthy__.
  </div>

  <a class="about-photo-link"
     href="{{ '/pdf/Recruitment/Welcome2OPTML.pdf' | relative_url }}"
     target="_blank"
     aria-label="Open Welcome2OPTML Booklet (PDF)">
    <img class="about-photo"
         src="{{ '/images/cover_img.png' | relative_url }}"
         alt="OPTML @ MSU">
  </a>
</div>

📖 **For a more detailed introduction, see our [Welcome2OPTML Booklet](/pdf/Recruitment/Welcome2OPTML.pdf).**


<div markdown="0" id="carousel" class="carousel slide" data-ride="carousel" data-interval="4000" data-pause="hover" >
    <!-- Menu -->
    <ol class="carousel-indicators">
        <li data-target="#carousel" data-slide-to="0" class="active"></li>
        <li data-target="#carousel" data-slide-to="1"></li>
        <li data-target="#carousel" data-slide-to="2"></li>
        <li data-target="#carousel" data-slide-to="3"></li>
        <li data-target="#carousel" data-slide-to="4"></li>
        <li data-target="#carousel" data-slide-to="5"></li>
        <li data-target="#carousel" data-slide-to="6"></li>
        <li data-target="#carousel" data-slide-to="7"></li>
        <li data-target="#carousel" data-slide-to="8"></li>
        <li data-target="#carousel" data-slide-to="9"></li>
    </ol>

    <!-- Items -->
    <div class="carousel-inner" markdown="0">
        <div class="item active">
            <img src="{{ site.url }}{{ site.baseurl }}/images/slider/logo.png" alt="Slide 1" />
        </div>
        <div class="item">
            <img src="{{ site.url }}{{ site.baseurl }}/images/slider/campus4.jpeg" alt="Slide 2" />
        </div>
        <div class="item">
            <img src="{{ site.url }}{{ site.baseurl }}/images/slider/campus3.jpeg" alt="Slide 3" />
        </div>
        <div class="item">
            <img src="{{ site.url }}{{ site.baseurl }}/images/slider/campus5.jpeg" alt="Slide 4" />
        </div>
        <div class="item">
            <img src="{{ site.url }}{{ site.baseurl }}/images/slider/campus1.jpeg" alt="Slide 5" />
        </div>       
        <div class="item">
            <img src="{{ site.url }}{{ site.baseurl }}/images/slider/campus2.jpeg" alt="Slide 6" />
        </div>
        <div class="item">
            <img src="{{ site.url }}{{ site.baseurl }}/images/slider/campus7.jpeg" alt="Slide 7" />
        </div>
        <div class="item">
            <img src="{{ site.url }}{{ site.baseurl }}/images/slider/campus8.jpeg" alt="Slide 8" />
        </div>
        <div class="item">
            <img src="{{ site.url }}{{ site.baseurl }}/images/slider/campus9.jpeg" alt="Slide 9" />
        </div>
        <div class="item">
            <img src="{{ site.url }}{{ site.baseurl }}/images/slider/campus10.jpeg" alt="Slide 10" />
        </div>
    </div>
  <a class="left carousel-control" href="#carousel" role="button" data-slide="prev">
    <span class="glyphicon glyphicon-chevron-left" aria-hidden="true"></span>
    <span class="sr-only">Previous</span>
  </a>
  <a class="right carousel-control" href="#carousel" role="button" data-slide="next">
    <span class="glyphicon glyphicon-chevron-right" aria-hidden="true"></span>
    <span class="sr-only">Next</span>
  </a>
</div>

As AI moves from the lab into the real world (e.g., autonomous vehicles), ensuring its safety becomes a paramount requirement prior to its deployment. Moreover, as datasets, ML/DL models, and learning tasks become increasingly complex, getting ML/DL to scale calls for new advances in learning algorithm design. More broadly, the study towards robust and scalable AI could make a significant impact on machine learning theories, and induce more promising applications in, e.g., automated ML, meta-learning, privacy and security, hardware design, and big data analysis. We seek a new learning frontier when the current learning algorithms become infeasible, and formalize foundations of secure learning.

**We always look for passionate students to join the team in terms of RA/TA/externship/internship/visiting students** [(more info)]({{ site.url }}{{ site.baseurl }}/vacancies)**!**


### Representative Publications

Authors marked in **bold** indicate our group members, and "\*" indicates equal contribution.<br/>

**Trustworthy AI: Robustness, fairness, and model explanation**

* [The Fragile Truth of Saliency: Improving LLM Input Attribution via Attention Bias Optimization](https://openreview.net/pdf?id=DrUR87D4Hj)<br>**Y. Zhang**, **C. Wang**, **Y. Chen**, **C. Fan**, **J. Jia**, **S. Liu**, <br> NeurIPS’25 **<span style="color:red">(Spotlight)</span>**

* [Rethinking Machine Unlearning for Large Language Models](https://www.nature.com/articles/s42256-025-00985-0)<br>**S. Liu**, Y. Yao, **J. Jia**, S. Casper, N. Baracaldo, P. Hase, **Y. Yao**, C. Y. Liu, X. Xu, H. Li, K. R. Varshney, M. Bansal, S. Koyejo, Y. Liu<br> Nature Machine Intelligence, 2025.

* [Salun: Empowering Machine Unlearning Via Gradient-based Weight Saliency In Both Image Classification And Generation](https://arxiv.org/pdf/2310.12508)<br>**C. Fan\***, **J. Liu\***, **Y. Zhang**, E. Wong, D. Wei, **S. Liu**<br> ICLR’24 **<span style="color:red">(Spotlight)</span>**

* [Model sparsification can simplify machine unlearning](https://arxiv.org/abs/2304.04934)<br>
    **J. Jia\***, **J. Liu\***, P. Ram, **Y. Yao**, G. Liu, Y. Liu, P. Sharma, **S. Liu**<br>
    NeurIPS’23 **<span style="color:red">(Spotlight)</span>**

<!-- * [Understanding and Improving Visual Prompting: A Label-Mapping Perspective](https://arxiv.org/abs/2209.10222)<br>
    **A. Chen**, **Y. Yao**, P.-Y. Chen, **Y. Zhang**, **S. Liu**<br>
    CVPR’23 -->

* [Revisiting and advancing fast adversarial training through the lens of bi-level optimization](https://arxiv.org/abs/2112.12376)<br>
    **Y. Zhang\***, G. Zhang\*, P. Khanduri, M. Hong, S. Chang, **S. Liu**<br>
    ICML’22

* [How to Robustify Black-Box ML Models? A Zeroth-Order Optimization Perspective](https://arxiv.org/abs/2203.14195)<br>
    **Y. Zhang**, **Y. Yao**, **J. Jia**, J. Yi, M. Hong, S. Chang, **S. Liu**<br>
    ICLR’22 **<span style="color:red">(Spotlight)</span>**

* [Reverse Engineering of Imperceptible Adversarial Image Perturbations](https://arxiv.org/abs/2203.14145)<br>
    Y. Gong\*, **Y. Yao\***, Y. Li, Y. Zhang, X. Liu, X. Lin, **S. Liu**<br>
    ICLR’22


**Scalable AI: Model & data compression, distributed learning, black-box optimization, and automated ML**

* [Selectivity Drives Productivity: Efficient Dataset Pruning for Enhanced Transfer Learning](https://arxiv.org/abs/2310.08782)<br>
    **Y. Zhang\***, **Y. Zhang\***, **A. Chen**, **J. Jia**, **J. Liu**, G. Liu, M. Hong, S. Chang, **S. Liu**<br>
    NeurIPS’23

* [Advancing Model Pruning via Bi-level Optimization](https://arxiv.org/abs/2210.04092)<br>
    **Y. Zhang\***, **Y. Yao\***, P. Ram, P. Zhao, T. Chen, M. Hong, Y. Wang, **S. Liu**<br>
    NeurIPS’22

* [Distributed Adversarial Training to Robustify Deep Neural Networks at Scale](https://arxiv.org/abs/2206.06257)<br>
    G. Zhang\*, S. Lu\*, **Y. Zhang**, X. Chen, P.-Y. Chen, Q. Fan, L. Martie, L. Horesh, M. Hong, **S. Liu**<br>
    UAI’22 **<span style="color:red">(Best Paper Runner-Up Award)</span>**

* [Min-Max Optimization without Gradients: Convergence and Applications to Adversarial ML](https://arxiv.org/abs/1909.13806)<br>
    **S. Liu**, S. Lu, X. Chen, Y. Feng, K. Xu, A. Al-Dujaili, M. Hong, U.-M. O'Reilly<br>
    ICML’20

* [A Primer on Zeroth-Order Optimization in Signal Processing and Machine Learning](https://arxiv.org/abs/2006.06224)<br>
    **S. Liu**, P.-Y. Chen, B. Kailkhura, G. Zhang, A. O. Hero, P. K. Varshney<br>
    IEEE Signal Processing Magazine, 2020

### Sponsors

We are grateful for funding from [Michigan State University](https://msu.edu), [MIT-IBM Watson AI Lab](https://mitibmwatsonailab.mit.edu/), [DARPA](https://www.darpa.mil/), [Cisco Research](https://research.cisco.com/), [NSF](https://www.nsf.gov/), [DSO National Laboratories](https://www.dso.org.sg/), [LLNL](https://www.llnl.gov/), [ARO](https://www.arl.army.mil/who-we-are/aro/), [Amazon Research](https://www.amazon.science/), [Open Philanthropy](https://www.openphilanthropy.org/), [Schmidt Sciences](https://www.schmidtsciences.org/) and [CAIS (Center for AI Safety)](https://safe.ai/).

<center>
<figure class="fourth">
  <img src="{{ site.url }}{{ site.baseurl }}/images/logopic/Logo_ibm.png" style="width: 30%" padding="5% 5% 5% 5%">
  <img src="{{ site.url }}{{ site.baseurl }}/images/logopic/Logo_DARPA.jpeg" style="width: 30%" padding="5% 5% 5% 5%">
  <img src="{{ site.url }}{{ site.baseurl }}/images/logopic/Logo_Cisco.png" style="width: 30%" padding="5% 5% 5% 5%">
</figure>

<figure class="fourth">
<img src="{{ site.url }}{{ site.baseurl }}/images/logopic/Logo_NSF.png" style="width: 30%" padding="5% 5% 5% 5%">
<img src="{{ site.url }}{{ site.baseurl }}/images/logopic/Logo_DSO.png" style="width: 30%" padding="5% 5% 5% 5%">
<img src="{{ site.url }}{{ site.baseurl }}/images/logopic/Logo_LLNL.png" style="width: 30%" padding="5% 5% 5% 5%">
</figure>

<figure class="fourth">
<img src="{{ site.url }}{{ site.baseurl }}/images/logopic/Logo_ARO.png" style="width: 30%" padding="5% 5% 5% 5%">
<img src="{{ site.url }}{{ site.baseurl }}/images/logopic/Logo_Amazon.png" style="width: 30%" padding="5% 5% 5% 5%">
<img src="{{ site.url }}{{ site.baseurl }}/images/logopic/Logo_open_philanthropy.png" style="width: 30%" padding="5% 5% 5% 5%">
</figure>

<figure class="fourth">
  <img src="{{ site.url }}{{ site.baseurl }}/images/logopic/Logo_cais.png"
       style="height: 120px; width: auto; padding: 5%; object-fit: contain;">
  <img src="{{ site.url }}{{ site.baseurl }}/images/logopic/Logo_schmidt.png"
       style="height: 120px; width: auto; padding: 5%; object-fit: contain;">
  <span style="display:inline-block; width: 30%; padding: 5%;"></span>
</figure>

</center>

<br/> 

<center>
    <script type="text/javascript" id="clstr_globe" src="//clustrmaps.com/globe.js?w=150&d=TYai0XCoTewd2PjwgwCME3t_ufoIcL1VJH0Y31jPsAA"></script>
</center>
