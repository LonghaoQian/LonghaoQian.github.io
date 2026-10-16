---
layout: page
title: projects
permalink: /projects/
description: Research, competition, and industry projects. Click a card for the full description.
nav: true
nav_order: 3
lang: en
display_categories: [research, competition, industry]
horizontal: false
---

<style>
  /* Full project titles are long; keep the cards compact. */
  .projects .card-title { font-size: 1.15rem; line-height: 1.35; }
</style>

<!-- pages/projects.md: lists the projects whose `lang` matches this page -->
<div class="projects">
{% assign lang_projects = site.projects | where: "lang", page.lang %}
{% for category in page.display_categories %}
  <a id="{{ category }}" href=".#{{ category }}">
    <h2 class="category">{{ category }}</h2>
  </a>
  {% assign categorized_projects = lang_projects | where: "category", category %}
  {% assign sorted_projects = categorized_projects | sort: "importance" %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in sorted_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
{% endfor %}
</div>
