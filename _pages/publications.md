---
layout: page
permalink: /publications/
title: publications
description: Publications in reversed chronological order.
years: [2021, 2020, 2019]
nav: true
nav_order: 2
scholar:
  bibliography_template: bib
  group_by: year
  group_order: descending
---

\* denotes equal contribution.

<!-- _pages/publications.md -->
<div class="publications">

{%- for y in page.years %}
  <h2 class="year">{{y}}</h2>
  {% bibliography -f {{ site.scholar.bibliography }} -q @*[year={{y}}]* --template bib %}
{% endfor %}

</div>
