---
layout: page
permalink: /cv/
title: CV
description: Curriculum vitae. The project descriptions below are the same as on the research and industrial experience pages.
nav: true
nav_order: 6
lang: en
toc:
  sidebar: left
---

{% assign email = site.data.socials.email %}

{% include cv_download.liquid pdf='/assets/cv/Longhao_Qian_CV_EN.pdf' label='Download PDF' %}

## Personal information

<table class="table table-sm table-borderless">
  <tr><td><strong>Name</strong></td><td>Longhao Qian (潜龙昊)</td></tr>
  <tr><td><strong>Highest degree</strong></td><td>Ph.D.</td></tr>
  <tr><td><strong>Current location</strong></td><td>Toronto, Canada</td></tr>
  <tr><td><strong>Profiles</strong></td><td>
    LinkedIn: <a href="https://www.linkedin.com/in/longhao-qian-uoft-postdoc/">linkedin.com/in/longhao-qian-uoft-postdoc</a><br>
    GitHub: <a href="https://github.com/LonghaoQian">github.com/LonghaoQian</a><br>
    Google Scholar: <a href="https://scholar.google.ca/citations?hl=en&user=p2oGLVYAAAAJ">scholar.google.ca/citations?user=p2oGLVYAAAAJ</a>
  </td></tr>
  <tr><td><strong>Email</strong></td><td><a href="mailto:{{ email | encode_email }}">{{ email }}</a></td></tr>
</table>

## Summary

{{ site.data.profile.en.summary | markdownify }}

## Work and project experience

### Postdoctoral Researcher — University of Toronto, Institute for Aerospace Studies

**2025/11 – present** · [www.utias.utoronto.ca](https://www.utias.utoronto.ca/) · Lab: [Flight Systems and Control (FSC) Lab](https://flight.utias.utoronto.ca/) · 4925 Dufferin St, North York, ON M3H 5T6, Canada

**Supervisor:** Dr. Hugh H.T. Liu — Fellow of the Canadian Academy of Engineering; Professor and Ph.D. supervisor at the University of Toronto Institute for Aerospace Studies; Director of the University of Toronto Centre for Aerial Robotics Research and Education.

**Work achievements:**

{% assign cv_projects = site.projects | where: "lang", page.lang | where: "cv_group", "utias-postdoc" | sort: "importance" %}
{% for p in cv_projects %}

#### Project: [{{ p.title }}]({{ p.url | relative_url }})

_{{ p.period }}_

{{ p.content | split: '<!-- details -->' | last }}
{% endfor %}

### Chip Software Engineer — Huawei Technologies Co., Ltd.

**2021/06 – 2023/04** · Job grade: 16 · [Huawei Shanghai Research Center](https://www.huawei.com/en/media-center/multimedia/photos/facilities/shanghai-research-center) · Huawei Shanghai Research Institute, 2222 Xinjinqiao Road, Jinqiao Economic and Technological Development Zone, Shanghai, China

**Work achievements:**

{% assign cv_projects = site.projects | where: "lang", page.lang | where: "cv_group", "huawei" %}
{% for p in cv_projects %}
{{ p.content | split: '<!-- details -->' | last }}
{% endfor %}

### Ph.D. — University of Toronto, Institute for Aerospace Studies

**2016/09 – 2021/03** · [www.utias.utoronto.ca](https://www.utias.utoronto.ca/) · Lab: [Flight Systems and Control (FSC) Lab](https://flight.utias.utoronto.ca/) · 4925 Dufferin St, North York, ON M3H 5T6, Canada

**Supervisor:** Dr. Hugh H.T. Liu — Fellow of the Canadian Academy of Engineering; Professor and Ph.D. supervisor at the University of Toronto Institute for Aerospace Studies; Director of the University of Toronto Centre for Aerial Robotics Research and Education.

**Work achievements:**

{% assign cv_projects = site.projects | where: "lang", page.lang | where: "cv_group", "utias-phd" %}
{% for p in cv_projects %}
{{ p.content | split: '<!-- details -->' | last }}
{% endfor %}

### Software Algorithm R&D Engineer (remote) — CNTech, Zhongfang Intelligent Technology (Shanghai) Co., Ltd.

**2016/02 – 2020/09** · [www.cntech.com](http://www.cntech.com/) · Zhongfang Building, Lingang Songjiang Science and Technology City, 1005 Jiuxin Road, Songjiang District, Shanghai, China (near Shunqing Road)

**Work achievements:**

{% assign cv_projects = site.projects | where: "lang", page.lang | where: "cv_group", "cntech" %}
{% for p in cv_projects %}
{{ p.content | split: '<!-- details -->' | last }}
{% endfor %}

## Education

- **2016/09 – 2021/03 · Ph.D., Aerospace Science and Engineering**<br>
  University of Toronto, Institute for Aerospace Studies<br>
  Supervisor: Dr. Hugh H.T. Liu — Fellow of the Canadian Academy of Engineering; Professor and Ph.D. supervisor at the University of Toronto Institute for Aerospace Studies; Director of the University of Toronto Centre for Aerial Robotics Research and Education.
- **2013/09 – 2016/03 · Master's degree, Aeronautical and Astronautical Science and Technology**<br>
  Shanghai Jiao Tong University, School of Aeronautics and Astronautics<br>
  Supervisor: Prof. Shiqiang Hu — Vice Dean and Party Secretary of the School of Aeronautics and Astronautics, Shanghai Jiao Tong University; Professor and Ph.D. supervisor.
- **2014/01 – 2014/12 · Master's degree, Aerospace Engineering**<br>
  University of Toronto, Institute for Aerospace Studies<br>
  Supervisor: Dr. Hugh H.T. Liu — Fellow of the Canadian Academy of Engineering; Professor and Ph.D. supervisor at the University of Toronto Institute for Aerospace Studies; Director of the University of Toronto Centre for Aerial Robotics Research and Education.
- **2009/09 – 2013/06 · Bachelor's degree, Aeronautical Engineering**<br>
  Shanghai Jiao Tong University, School of Aeronautics and Astronautics
- **2011/09 – 2013/06 · Second bachelor's degree, Applied Electronic Technology**<br>
  Shanghai Jiao Tong University, School of Aeronautics and Astronautics

## Publications

### Published / accepted

<div class="publications">

{% bibliography --group_by none --query @*[status!=review] %}

</div>

### Under review

<div class="publications">

{% bibliography --group_by none --query @*[status=review] %}

</div>

## Teaching

{% include teaching_list.liquid lang=page.lang %}

## Conference presentations

| Conference                                                                         | Date       | Role         |
| ---------------------------------------------------------------------------------- | ---------- | ------------ |
| IEEE 10th World Forum on Internet of Things                                        | 2024/11/11 | Presentation |
| Canadian Aeronautics and Space Institute (CASI) AERO 2023                          | 2023/11/15 | Presentation |
| IEEE 9th World Forum on Internet of Things                                         | 2023/10/12 | Presentation |
| 2023 AIAA Science and Technology Forum and Exposition (AIAA SciTech Forum)         | 2023/01/23 | Presentation |
| IEEE/ASME International Conference on Advanced Intelligent Mechatronics (AIM) 2020 | 2020/07/06 | Presentation |
| 2019 AIAA Science and Technology Forum and Exposition (AIAA SciTech Forum)         | 2019/01/06 | Presentation |
| 8th Conference on Systems and Control Theory                                       | 2018/05/07 | Presentation |
| Canadian Conference on Electrical and Computer Engineering (CCECE) 2017            | 2017/04/30 | Presentation |

## Professional service

### Memberships of international societies

| Society                                                   | Membership | Validity |
| --------------------------------------------------------- | ---------- | -------- |
| Institute of Electrical and Electronics Engineers (IEEE)  | Member     | Ongoing  |
| American Institute of Aeronautics and Astronautics (AIAA) | Member     | Ongoing  |

### Reviewer for international journals and conferences (110 reviews in total)

**Journals:** AIAA Journal of Guidance, Control, and Dynamics · IEEE Transactions on Industrial Electronics · IEEE Transactions on Systems, Man, and Cybernetics: Systems · IEEE Transactions on Control Systems Technology · IEEE Transactions on Automatic Control · IEEE/ASME Transactions on Mechatronics · IEEE Transactions on Aerospace and Electronic Systems · IEEE Transactions on Intelligent Vehicles · IEEE Robotics and Automation Letters · IEEE Transactions on Robotics · Unmanned Systems · Journal of Aerospace Engineering · International Journal of Aerospace Engineering · Aerospace Science and Technology · Journal of Systems and Control Engineering · Drones

**Conferences:** IEEE International Conference on Robotics and Automation (ICRA) · IEEE Conference on Decision and Control (CDC) · IEEE Canadian Conference on Electrical and Computer Engineering (CCECE) · American Control Conference (ACC)

### Conference program committees

- The 23rd IEEE International Conference on Industrial Informatics (INDIN 2025) — Track Program Committee (TPC) reviewer (Factory Communications, Control and Automation Systems)
- 2025 IEEE 11th World Forum on Internet of Things (WF-IoT 2025) — Track Program Committee (TPC) reviewer

## Awards

### Industry awards

| Date    | Award                                          |
| ------- | ---------------------------------------------- |
| 2023/04 | Huawei annual performance evaluation: A rating |
| 2023/01 | HiSilicon Quality Star Award (Huawei)          |
| 2021/08 | HiSilicon New Star Award (Huawei)              |

### Scholarships

| Date    | Institution                   | Scholarship                                                                                               |
| ------- | ----------------------------- | --------------------------------------------------------------------------------------------------------- |
| 2017/02 | University of Toronto         | Ontario Trillium Scholarship (only 75 recipients across Ontario; C$160,000 in total, approx. RMB 820,000) |
| 2011/09 | Shanghai Jiao Tong University | Shanghai Jiao Tong University Third-Class Scholarship                                                     |
| 2010/09 | Shanghai Jiao Tong University | Shanghai Jiao Tong University Third-Class Scholarship                                                     |
| 2010/03 | Shanghai Jiao Tong University | Shanghai Jiao Tong University Third-Class Scholarship                                                     |

### Academic contribution awards

| Year | Award                                                                        |
| ---- | ---------------------------------------------------------------------------- |
| 2024 | Excellent Reviewer for the Journal of Guidance, Control, and Dynamics (JGCD) |
| 2022 | Excellent Reviewer for the Journal of Guidance, Control, and Dynamics (JGCD) |
