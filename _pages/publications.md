---
title: "OPTML Group - Publications"
layout: gridlay
# excerpt: "OPTML Group -- Publications."
sitemap: false
permalink: /publications
---


# Publications

Authors marked in <span style="color:blue">blue</span> indicate our group members, and "\*" indicates equal contribution.<br />
Jump: [Preprints](#preprints), [Conference Papers](#highlighted-conference-papers) and [Journal Papers](#journal-papers)



## Highlighted Conference Papers

**Back to [Top](#publications)**

{% for publi in site.data.publications.conferences %}

  <a href="{{ publi.link.url }}"><b>{{ publi.title }}</b></a> <br />
  <em>{{ publi.authors }} </em><br />
  {{ publi.link.display }}

{% endfor %}

## Journal Papers

**Back to [Top](#publications)**

{% for publi in site.data.publications.journals %}

  <a href="{{ publi.link.url }}"><b>{{ publi.title }}</b></a> <br />
  <em>{{ publi.authors }} </em><br />
  {{ publi.link.display }}

{% endfor %}
