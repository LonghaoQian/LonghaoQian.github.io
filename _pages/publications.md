---
layout: page
permalink: /publications/
title: publications
description: Published and accepted papers in reverse chronological order, followed by papers under review. “CAS Zone 1” refers to the top tier of the Chinese Academy of Sciences journal ranking; “JCR Q1” to the top quartile of Clarivate's Journal Citation Reports.
nav: true
nav_order: 2
lang: en
---

<!-- _pages/publications.md -->

<!-- Bibsearch Feature -->

{% include bib_search.liquid %}

<div class="publications">

{% bibliography --query @*[status!=review] %}

<h2 class="bibliography">under review</h2>

{% bibliography --group_by none --query @*[status=review] %}

</div>
