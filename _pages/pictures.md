---
title: "OPTML - Photos"
layout: piclay
excerpt: "OPTML -- Photos"
permalink: /pictures/
---

<style>
  .image-gallery {overflow: auto; margin-left: 0%!important;}
  .image-gallery a {float: left; display: block; margin: 0 0 0.5% 0.5%; width: 30%; text-align: center; text-decoration: none!important;}
  .image-gallery a span {display: block; text-overflow: ellipsis; overflow: hidden; white-space: nowrap; padding: 3px 0;}
  .image-gallery a img {width: 100%; display: block; margin-bottom: 0%!important; padding-top: 0px;}
  .image-gallery a:first-child {padding-top: 0px}
</style>


## Photos
Dive into the journey of OPTML. Explore our academic pursuits, cherishable memories, the culinary delights of MSU, our candid moments, and the majestic landscapes of the MSU campus.

Jump to: [Group Academic Activities](#group-academic-activities), [Life Beyond Research](#life-beyond-research), [MSU Culinary Delights](#msu-culinary-delights), [Candid Chronicles](#candid-chronicles), [MSU's Serene Beauty](#msus-serene-beauty), [Group Logos](#group-logos)


### Life Beyond Research

Experience our passion for research and academic excellence. Be a part of the conferences, seminars, and workshops that have shaped our group's intellectual trajectory.

<div class="image-gallery">

<a/>

{% for pic in site.data.pictures.conference %}

  <a href="{{ site.url }}{{ site.baseurl }}/{{ pic.image }}" title="{{ pic.title }}">
    <img src="//images.weserv.nl/?url=www.optml-group.com/{{ pic.image }}&w=300&h=300&output=jpg&q=50&t=square" alt="{{ pic.title }}" />
    <span>{{ pic.title }}</span>
  </a>

{% endfor %}
</div>

Go back to [Top](#photos).

### Group Life Photos


<div class="image-gallery">

<a/>

{% for pic in site.data.pictures.life %}

  <a href="{{ site.url }}{{ site.baseurl }}/{{ pic.image }}" title="{{ pic.title }}">
    <img src="//images.weserv.nl/?url=www.optml-group.com/{{ pic.image }}&w=300&h=300&output=jpg&q=50&t=square" alt="{{ pic.title }}" />
    <span>{{ pic.title }}</span>
  </a>

{% endfor %}
</div>

Go back to [Top](#photos).


### MSU Culinary Delights


<div class="image-gallery">

<a/>

{% for pic in site.data.pictures.food %}

  <a href="{{ site.url }}{{ site.baseurl }}/{{ pic.image }}" title="{{ pic.title }}">
    <img src="//images.weserv.nl/?url=www.optml-group.com/{{ pic.image }}&w=300&h=300&output=jpg&q=50&t=square" alt="{{ pic.title }}" />
    <span>{{ pic.title }}</span>
  </a>

{% endfor %}
</div>

Go back to [Top](#photos).


### Candid Chronicles

A collection of spontaneous, unscripted moments that capture the essence of our group's spirit and camaraderie. Laughter guaranteed!


<div class="image-gallery">

<a/>

{% for pic in site.data.pictures.funny %}

  <a href="{{ site.url }}{{ site.baseurl }}/{{ pic.image }}" title="{{ pic.title }}">
    <img src="//images.weserv.nl/?url=www.optml-group.com/{{ pic.image }}&w=300&h=300&output=jpg&q=50&t=square" alt="{{ pic.title }}" />
    <span>{{ pic.title }}</span>
  </a>

{% endfor %}
</div>

Go back to [Top](#photos).


### MSU's Serene Beauty

Embark on a visual journey across the verdant and picturesque MSU campus. Witness nature's splendor in the heart of an academic institution. Go Green! Go White!

<div class="image-gallery">

<a/>

{% for pic in site.data.pictures.msu_campus %}

  <a href="{{ site.url }}{{ site.baseurl }}/{{ pic.image }}" title="{{ pic.title }}">
    <img src="//images.weserv.nl/?url=www.optml-group.com/{{ pic.image }}&w=300&h=300&output=jpg&q=50&t=square" alt="{{ pic.title }}" />
    <span>{{ pic.title }}</span>
  </a>

{% endfor %}
</div>

Go back to [Top](#photos).


### Group Logos
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

<!-- #### group T-shirt
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
</center> -->