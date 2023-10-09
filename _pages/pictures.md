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


# Photos
Jump to: [Group Academic Activities](#group-academic-activities), [Group Life Photos](#group-life-photos), [Food at MSU](#food-at-msu), [Group Funny Moments](#group-funny-moments), [MSU Campus](#beautiful-campus-of-msu-go-green), [Group Logos](#group-logos)


## OPTML Academic Activities

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

## Group Life Photos


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


## Food at MSU


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


## Group Funny Moments


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


## Beautiful Campus of MSU! Go Green!

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