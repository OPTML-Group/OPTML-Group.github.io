---
title: "OTML - Pictures"
layout: piclay
excerpt: "OTML -- Pictures"
permalink: /pictures/
---

# Pictures
Jump to: [Adversarial T-shirt](#adversarial-t-shirt), [MSU Campus](#beautiful-campus-of-msu!-go-green!), [Group Logos](#group-logos)

## Adversarial T-shirt
#### K. Xu, G. Zhang, S. Liu, Q. Fan, M. Sun, H. Chen, P.-Y. Chen, Y. Wang, X. Lin, [Adversarial T-shirt! Evading Person Detectors in A Physical World](https://www.ecva.net/papers/eccv_2020/papers_ECCV/papers/123500647.pdf), ECCV’20
<center> <iframe weight="600" height="300" src="https://www.youtube.com/embed/8GCN7xQkaa0" frameborder="0" allowfullscreen></iframe> </center>

## Beautiful Campus of MSU! Go Green!

(Right-click *'view image'* to see a larger image.)
{% assign number_printed = 0 %}
{% for pic in site.data.pictures_Leiden %}

{% assign even_odd = number_printed | modulo: 4 %}

{% if even_odd == 0 %}
<div class="row">
{% endif %}

<div class="col-sm-3 clearfix">
<img src="{{ site.url }}{{ site.baseurl }}/images/picpic/campus/{{ pic.image }}" class="img-responsive" width="95%" style="float: left" />
</div>

{% assign number_printed = number_printed | plus: 1 %}

{% if even_odd > 2 %}
</div>
{% endif %}


{% endfor %}

{% assign even_odd = number_printed | modulo: 4 %}
{% if even_odd == 1 %}
</div>
{% endif %}

{% if even_odd == 2 %}
</div>
{% endif %}

{% if even_odd == 3 %}
</div>
{% endif %}

<p> &nbsp; </p>

#### Cute Dr. Squirrel on compus!
<center> <iframe width="600" height="300" src="https://www.youtube.com/embed/scQs0zwvrfk" frameborder="0" allowfullscreen></iframe> </center>

## Group Logos
#### group logo
<center>
<figure>
<img src="{{ site.url }}{{ site.baseurl }}/images/picpic/logo.png" width="60%">
</figure>
</center>

#### group logo - black
<center>
<figure>
<img src="{{ site.url }}{{ site.baseurl }}/images/picpic/logo_black.png" width="60%">
</figure>
</center>

#### group logo - white
<center>
<figure>
<img src="{{ site.url }}{{ site.baseurl }}/images/picpic/logo_white.png" width="60%">
</figure>
</center>

#### group T-shirt
<center>
<figure>
<img src="{{ site.url }}{{ site.baseurl }}/images/picpic/group_tshirt.png" width="60%">
</figure>
</center>

#### group sign
<center>
<figure>
<img src="{{ site.url }}{{ site.baseurl }}/images/picpic/group_sign.png" width="60%">
</figure>
</center>

#### group icon
<center>
<figure>
<img src="{{ site.url }}{{ site.baseurl }}/images/picpic/group_icon.png" width="60%">
</figure>
</center>