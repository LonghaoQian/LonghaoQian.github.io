---
layout: page
permalink: /zh/publications/
title: 学术成果
description: 已发表/录用的论文按时间倒序排列，正在审稿的论文列于最后。
nav: true
nav_order: 2
lang: zh-CN
---

<!-- _pages/zh/publications.md -->

{% include bib_search.liquid %}

<div class="publications">

{% bibliography --file papers_zh --query @*[status!=review] %}

<h2 class="bibliography">正在审稿</h2>

{% bibliography --file papers_zh --group_by none --query @*[status=review] %}

</div>
