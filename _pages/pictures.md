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
Jump to: [Group Academic Activities](#group-academic-activities), [Group Life Photos](#group-life-photos), [MSU Campus](#beautiful-campus-of-msu-go-green), [Group Logos](#group-logos)


## OPTML Academic Activities

<div class="image-gallery">

{% for pic in site.data.pictures.conference %}

  <a href="{{ site.url }}{{ site.baseurl }}/{{ pic.image }}" title="{{ pic.title }}">
    <img src="//images.weserv.nl/?url=www.optml-group.com/{{ pic.image }}&w=300&h=300&output=jpg&q=50&t=square" alt="{{ pic.title }}" />
    <span>{{ pic.title }}</span>
  </a>

{% endfor %}
</div>


## Beautiful Campus of MSU! Go Green!

<div class="image-gallery">

{% for pic in site.data.pictures.msu_campus %}

  <a href="{{ site.url }}{{ site.baseurl }}/{{ pic.image }}" title="{{ pic.title }}">
    <img src="//images.weserv.nl/?url=www.optml-group.com/{{ pic.image }}&w=300&h=300&output=jpg&q=50&t=square" alt="{{ pic.title }}" />
    <span>{{ pic.title }}</span>
  </a>

{% endfor %}
</div>


<style>
#life .carousel-inner img {
  width: 100%; /* Adjust as needed */
  height: 500px; /* Adjust as needed */
  object-fit: cover; /* Cover the entire element box */
}
</style>


## Group Life Photos


<div markdown="0" id="life" class="carousel slide" data-ride="carousel" data-interval="4000" data-pause="hover" >
    <!-- Menu -->
    <ol class="carousel-indicators">
        <li data-target="#life" data-slide-to="0" class="active"></li>
        <li data-target="#life" data-slide-to="1"></li>
        <li data-target="#life" data-slide-to="2"></li>
        <li data-target="#life" data-slide-to="3"></li>
        <li data-target="#life" data-slide-to="4"></li>
        <li data-target="#life" data-slide-to="5"></li>
        <li data-target="#life" data-slide-to="6"></li>
        <li data-target="#life" data-slide-to="7"></li>
        <li data-target="#life" data-slide-to="8"></li>
        <li data-target="#life" data-slide-to="9"></li>
        <li data-target="#life" data-slide-to="10"></li>
        <li data-target="#life" data-slide-to="11"></li>
    </ol>

    <!-- Items -->
    <div class="carousel-inner" markdown="0">
        <div class="item active">
            <img src="{{ site.url }}{{ site.baseurl }}/images/picpic/group_pics/Life/pic1.jpg" alt="Slide 1" />
        </div>
        <div class="item">
            <img src="{{ site.url }}{{ site.baseurl }}/images/picpic/group_pics/Life/pic2.jpg" alt="Slide 2" />
        </div>
        <div class="item">
            <img src="{{ site.url }}{{ site.baseurl }}/images/picpic/group_pics/Life/pic3.jpg" alt="Slide 3" />
        </div>
        <div class="item">
            <img src="{{ site.url }}{{ site.baseurl }}/images/picpic/group_pics/Life/pic4.jpg" alt="Slide 4" />
        </div>
        <div class="item">
            <img src="{{ site.url }}{{ site.baseurl }}/images/picpic/group_pics/Life/pic5.jpg" alt="Slide 5" />
        </div>
        <div class="item">
            <img src="{{ site.url }}{{ site.baseurl }}/images/picpic/group_pics/Life/pic6.jpg" alt="Slide 6" />
        </div>
        <div class="item">
            <img src="{{ site.url }}{{ site.baseurl }}/images/picpic/group_pics/Life/pic7.jpg" alt="Slide 7" />
        </div>
        <div class="item">
            <img src="{{ site.url }}{{ site.baseurl }}/images/picpic/group_pics/Life/pic8.jpg" alt="Slide 8" />
        </div>
        <div class="item">
            <img src="{{ site.url }}{{ site.baseurl }}/images/picpic/group_pics/Life/pic9.jpg" alt="Slide 9" />
        </div>
        <div class="item">
            <img src="{{ site.url }}{{ site.baseurl }}/images/picpic/group_pics/Life/pic10.jpg" alt="Slide 10" />
        </div>
        <div class="item">
            <img src="{{ site.url }}{{ site.baseurl }}/images/picpic/group_pics/Life/pic11.jpg" alt="Slide 11" />
        </div>
        <div class="item">
            <img src="{{ site.url }}{{ site.baseurl }}/images/picpic/group_pics/Life/pic12.jpg" alt="Slide 12" />
        </div>
        <div class="item">
            <img src="{{ site.url }}{{ site.baseurl }}/images/picpic/group_pics/Life/pic13.jpg" alt="Slide 13" />
        </div>
        <div class="item">
            <img src="{{ site.url }}{{ site.baseurl }}/images/picpic/group_pics/Life/pic14.jpg" alt="Slide 14" />
        </div>
    </div>
  <a class="left carousel-control" href="#life" role="button" data-slide="prev">
    <span class="glyphicon glyphicon-chevron-left" aria-hidden="true"></span>
    <span class="sr-only">Previous</span>
  </a>
  <a class="right carousel-control" href="#life" role="button" data-slide="next">
    <span class="glyphicon glyphicon-chevron-right" aria-hidden="true"></span>
    <span class="sr-only">Next</span>
  </a>
</div>

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