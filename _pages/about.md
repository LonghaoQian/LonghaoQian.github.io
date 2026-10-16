---
layout: about
title: about
permalink: /
lang: en
subtitle: Postdoctoral Researcher, <a href='https://flight.utias.utoronto.ca/'>Flight Systems and Control (FSC) Lab</a>, <a href='https://www.utias.utoronto.ca/'>University of Toronto Institute for Aerospace Studies (UTIAS)</a>

profile:
  align: right
  image: prof_pic.jpg
  image_circular: false # crops the image to make it circular
  more_info: >
    <p>University of Toronto Institute for Aerospace Studies</p>
    <p>4925 Dufferin St, North York</p>
    <p>ON M3H 5T6, Canada</p>

selected_papers: true # includes a list of papers marked as "selected={true}"
social: true # includes social icons at the bottom of the page

announcements:
  enabled: false # includes a list of news items

latest_posts:
  enabled: false
---

{{ site.data.profile.en.bio | markdownify }}

More details: [projects]({{ '/projects/' | relative_url }}) · [publications]({{ '/publications/' | relative_url }}) · [teaching]({{ '/teaching/' | relative_url }}) · [CV]({{ '/cv/' | relative_url }})

{% include featured_projects.liquid heading='featured projects' url='/projects/' %}
