---
layout: page
permalink: /publications/
title: Publications
description: Publications in reversed chronological order. Alternatively, see my [Google Scholar](https://scholar.google.com/citations?user=vvr6LZkAAAAJ) or [Orcid](https://orcid.org/0000-0002-2219-6759) page.

years: [2021, 2020, 2019, 2016]
nav: true
---

<div class="publications">

{% for y in page.years %}
  <h2 class="year">{{y}}</h2>
  {% bibliography -f papers -q @*[year={{y}}]* %}
{% endfor %}

</div>
