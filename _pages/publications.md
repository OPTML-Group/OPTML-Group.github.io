---
title: "OTML Group - Publications"
layout: gridlay
excerpt: "OTML Group -- Publications."
sitemap: false
permalink: /publications
---


# Publications

Authors marked in <span style="color:blue">blue</span> indicate our group members, and "\*" indicates equal contribution.
Jump: [Conference Papers](#highlighted-conference-papers) and [Journal Papers](#journal-papers)

<!-- ## Group highlights

(For a full list of publications and patents see [below](#full-list-of-publications) or go to [Google Scholar](https://scholar.google.com/citations?user=C7dO_UgAAAAJ&hl=en).

{% assign number_printed = 0 %}
{% for publi in site.data.publist %}

{% assign even_odd = number_printed | modulo: 2 %}
{% if publi.highlight == 1 %}

{% if even_odd == 0 %}
<div class="row">
{% endif %}

<div class="col-sm-6 clearfix">
 <div class="well">
  <pubtit>{{ publi.title }}</pubtit>
  <img src="{{ site.url }}{{ site.baseurl }}/images/pubpic/{{ publi.image }}" class="img-responsive" width="100%" style="float: left" />
  <p>{{ publi.description }}</p>
  <p><em>{{ publi.authors }}</em></p>
  <p><strong><a href="{{ publi.link.url }}">{{ publi.link.display }}</a></strong></p>
  <p class="text-danger"><strong> {{ publi.news1 }}</strong></p>
  <p> {{ publi.news2 }}</p>
 </div>
</div>

{% assign number_printed = number_printed | plus: 1 %}

{% if even_odd == 1 %}
</div>
{% endif %}

{% endif %}
{% endfor %}

{% assign even_odd = number_printed | modulo: 2 %}
{% if even_odd == 1 %}
</div>
{% endif %}

<p> &nbsp; </p> -->

<!-- ## Full List of Publications -->

## Highlighted Conference Papers

**Back to [Top](#publications)**

{% for publi in site.data.publist %}

  <a href="{{ publi.link.url }}"><b>{{ publi.title }}</b></a> <br />
  <em>{{ publi.authors }} </em><br />
  {{ publi.link.display }}

{% endfor %}

## Journal Papers

**Back to [Top](#publications)**

{% for publi in site.data.journallist %}

  <a href="{{ publi.link.url }}"><b>{{ publi.title }}</b></a> <br />
  <em>{{ publi.authors }} </em><br />
  {{ publi.link.display }}

{% endfor %}
