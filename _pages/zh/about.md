---
layout: about
title: 首页
permalink: /zh/
lang: zh-CN
description: 潜龙昊（Longhao Qian），加拿大多伦多大学航空航天研究院（UTIAS）飞行系统与控制实验室博士后研究员，研究方向为无人机空中具身智能、强化学习与物理信息神经网络控制。
subtitle: 潜龙昊 · <a href='https://www.utias.utoronto.ca/'>加拿大多伦多大学航空航天研究院（UTIAS）</a><a href='https://flight.utias.utoronto.ca/'>飞行系统与控制实验室（FSC Lab）</a>博士后研究员

profile:
  align: right
  image: prof_pic.jpg
  image_circular: false
  more_info: >
    <p>多伦多大学航空航天研究院</p>
    <p>4925 Dufferin St, North York</p>
    <p>ON M3H 5T6, Canada</p>

# The about layout prints these two sections with English headings and links,
# so the Chinese home page renders them itself below.
selected_papers: false
social: false

announcements:
  enabled: false

latest_posts:
  enabled: false
---

{{ site.data.profile.zh.bio | markdownify }}

更多内容：[学术成果]({{ '/zh/publications/' | relative_url }}) · [科研项目]({{ '/zh/research/' | relative_url }}) · [工业界经历]({{ '/zh/industry/' | relative_url }}) · [授课经历]({{ '/zh/teaching/' | relative_url }}) · [个人简历]({{ '/zh/cv/' | relative_url }})

{% include featured_projects.liquid heading='代表性项目' url='/zh/research/' %}

<div class="social">
  <div class="contact-icons">{% social_links %}</div>
  <div class="contact-note">欢迎通过电子邮件与我联系。</div>
</div>
