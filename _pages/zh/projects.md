---
layout: page
title: 项目经历
permalink: /zh/projects/
description: 科研、竞赛与工业界项目。点击卡片查看完整介绍。
nav: true
nav_order: 3
lang: zh-CN
display_categories: [科研项目, 竞赛, 工业界项目]
horizontal: false
---

<style>
  /* Full project titles are long; keep the cards compact. */
  .projects .card-title { font-size: 1.15rem; line-height: 1.35; }
</style>

<!-- pages/zh/projects.md: lists the projects whose `lang` matches this page -->
<div class="projects">
{% assign lang_projects = site.projects | where: "lang", page.lang %}
{% for category in page.display_categories %}
  <a id="{{ category | slugify: 'raw' }}" href=".#{{ category | slugify: 'raw' }}">
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
