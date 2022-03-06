---
title: "Borglab - Pictures"
layout: piclay
excerpt: "Borglab -- Pictures"
permalink: /pictures/
---

# Pictures
Jump to: [Adversarial T-shirt](#adversarial-t-shirt)

## Adversarial T-shirt

#### 
<iframe width="560" height="315" src="https://youtu.be/8GCN7xQkaa0" frameborder="0" allowfullscreen></iframe>

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