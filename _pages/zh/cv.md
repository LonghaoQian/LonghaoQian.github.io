---
layout: page
permalink: /zh/cv/
title: 个人简历
description: 个人简历。以下项目介绍与“科研项目”和“工业界经历”页面内容一致。
nav: true
nav_order: 7
lang: zh-CN
toc:
  sidebar: left
---

{% assign email = site.data.socials.email %}

{% include cv_download.liquid pdf='/assets/cv/Longhao_Qian_CV_ZH.pdf' label='下载PDF简历' %}

## 个人信息

<table class="table table-sm table-borderless">
  <tr><td><strong>姓名</strong></td><td>潜龙昊（Longhao Qian）</td></tr>
  <tr><td><strong>最高学历</strong></td><td>博士</td></tr>
  <tr><td><strong>现居住地</strong></td><td>加拿大多伦多市</td></tr>
  <tr><td><strong>个人主页</strong></td><td>
    LinkedIn：<a href="https://www.linkedin.com/in/longhao-qian-uoft-postdoc/">linkedin.com/in/longhao-qian-uoft-postdoc</a><br>
    GitHub：<a href="https://github.com/LonghaoQian">github.com/LonghaoQian</a><br>
    谷歌学术：<a href="https://scholar.google.ca/citations?hl=en&user=p2oGLVYAAAAJ">scholar.google.ca/citations?user=p2oGLVYAAAAJ</a>
  </td></tr>
  <tr><td><strong>电子邮件</strong></td><td><a href="mailto:{{ email | encode_email }}">{{ email }}</a></td></tr>
</table>

## 个人综合评价

{{ site.data.profile.zh.summary | markdownify }}

## 工作与项目经历

### 博士后研究员 — University of Toronto, Institute for Aerospace Studies（多伦多大学航空航天研究院）

**2023/04至今** · 网站：[https://www.utias.utoronto.ca/](https://www.utias.utoronto.ca/) · 实验室：[飞行系统与控制实验室（FSC Lab）](https://flight.utias.utoronto.ca/) · 地址：4925 Dufferin St, North York, ON M3H 5T6, Canada

**导师：** Dr. Hugh H.T. Liu（刘洪涛教授），加拿大皇家工程院院士。加拿大多伦多大学航空航天学院教授、博导。多伦多大学空中机器人研究与教育中心主任。

**工作成果：**

{% assign cv_projects = site.projects | where: "lang", page.lang | where: "cv_group", "utias-postdoc" | sort: "importance" %}
{% for p in cv_projects %}

#### 课题：[{{ p.title }}]({{ p.url | relative_url }})

_{{ p.period }}_

{{ p.content | split: '<!-- details -->' | last | split: '<!-- end details -->' | first }}
{% endfor %}

### 芯片软件工程师 — 华为技术有限公司

**2021/06至2023/04** · 职级：16 · 网站：[华为上海研究所](https://www.huawei.com/en/media-center/multimedia/photos/facilities/shanghai-research-center) · 地址：华为上海研究所，金桥经济技术开发区新金桥路2222号

**工作成果：**

{% assign cv_projects = site.projects | where: "lang", page.lang | where: "cv_group", "huawei" %}
{% for p in cv_projects %}
{{ p.content | split: '<!-- details -->' | last | split: '<!-- end details -->' | first }}
{% endfor %}

### 博士 — University of Toronto, Institute for Aerospace Studies（多伦多大学航空航天研究院）

**2016/09至2021/03** · 网站：[https://www.utias.utoronto.ca/](https://www.utias.utoronto.ca/) · 实验室：[飞行系统与控制实验室（FSC Lab）](https://flight.utias.utoronto.ca/) · 地址：4925 Dufferin St, North York, ON M3H 5T6, Canada

**导师：** Dr. Hugh H.T. Liu（刘洪涛教授），加拿大皇家工程院院士。加拿大多伦多大学航空航天学院教授、博导。多伦多大学空中机器人研究与教育中心主任。

**工作成果：**

{% assign cv_projects = site.projects | where: "lang", page.lang | where: "cv_group", "utias-phd" %}
{% for p in cv_projects %}
{{ p.content | split: '<!-- details -->' | last | split: '<!-- end details -->' | first }}
{% endfor %}

### 软件算法研发工程师（远程） — 中仿智能科技（上海）股份有限公司

**2016/02至2020/09** · 网站：[http://www.cntech.com/](http://www.cntech.com/) · 地址：上海市松江区九新公路1005号临港松江科技城中仿大厦（近顺庆路）

**工作成果：**

{% assign cv_projects = site.projects | where: "lang", page.lang | where: "cv_group", "cntech" %}
{% for p in cv_projects %}
{{ p.content | split: '<!-- details -->' | last | split: '<!-- end details -->' | first }}
{% endfor %}

## 教育经历

- **2016/09至2021/03 · 博士 · Aerospace Science and Engineering（航空航天科学与工程）**<br>
  University of Toronto（加拿大多伦多大学）· Institute for Aerospace Studies（航空航天研究院）<br>
  导师：Dr. Hugh H.T. Liu（刘洪涛教授），加拿大皇家工程院院士。加拿大多伦多大学航空航天学院教授、博导。多伦多大学空中机器人研究与教育中心主任。
- **2013/09至2016/03 · 硕士 · 航空宇航科学与技术**<br>
  上海交通大学 · 航空航天学院<br>
  导师：胡士强，上海交通大学航空航天学院副院长、党委书记。教授、博导。
- **2014/01至2014/12 · 硕士 · Aerospace Engineering（航空航天工程）**<br>
  University of Toronto（加拿大多伦多大学）· Institute for Aerospace Studies（航空航天研究院）<br>
  导师：Dr. Hugh H.T. Liu（刘洪涛教授），加拿大皇家工程院院士。加拿大多伦多大学航空航天学院教授、博导。多伦多大学空中机器人研究与教育中心主任。
- **2009/09至2013/06 · 学士 · 航空工程**<br>
  上海交通大学 · 航空航天学院
- **2011/09至2013/06 · 学士第二学位 · 应用电子技术**<br>
  上海交通大学 · 航空航天学院

## 学术成果

### 已发表/录用

<div class="publications">

{% bibliography --file papers_zh --group_by none --query @*[status!=review] %}

</div>

### 正在审稿

<div class="publications">

{% bibliography --file papers_zh --group_by none --query @*[status=review] %}

</div>

## 授课经历

{% include teaching_list.liquid lang=page.lang %}

## 国际会议报告/演讲

| 会议名称                                                                           | 参会时间   | 参会角色 |
| ---------------------------------------------------------------------------------- | ---------- | -------- |
| IEEE 10th World Forum on Internet of Things                                        | 2024/11/11 | 演讲     |
| Canadian Aeronautics and Space Institute (CASI) AERO 2023                          | 2023/11/15 | 演讲     |
| IEEE 9th World Forum on Internet of Things                                         | 2023/10/12 | 演讲     |
| 2023 AIAA Science and Technology Forum and Exposition (AIAA SciTech Forum)         | 2023/01/23 | 演讲     |
| IEEE/ASME International Conference on Advanced Intelligent Mechatronics (AIM) 2020 | 2020/07/06 | 演讲     |
| 2019 AIAA Science and Technology Forum and Exposition (AIAA SciTech Forum)         | 2019/01/06 | 演讲     |
| 8th Conference on Systems and Control Theory                                       | 2018/05/07 | 演讲     |
| Canadian Conference on Electrical and Computer Engineering (CCECE) 2017            | 2017/04/30 | 演讲     |

## 专家职务

### 国际协会会员

| 协会                                                                            | 身份 | 有效期   |
| ------------------------------------------------------------------------------- | ---- | -------- |
| 国际电气电子工程师协会 Institute of Electrical and Electronics Engineers (IEEE) | 会员 | 长期有效 |
| 美国航空航天学会 American Institute of Aeronautics and Astronautics (AIAA)      | 会员 | 长期有效 |

### 担任国际期刊/会议评审专家（总审稿量：110篇）

**国际期刊：** AIAA Journal of Guidance, Control, and Dynamics · IEEE Transactions on Industrial Electronics · IEEE Transactions on Systems, Man, and Cybernetics: Systems · IEEE Transactions on Control Systems Technology · IEEE Transactions on Automatic Control · IEEE/ASME Transactions on Mechatronics · IEEE Transactions on Aerospace and Electronic Systems · IEEE Transactions on Intelligent Vehicles · IEEE Robotics and Automation Letters · IEEE Transactions on Robotics · Unmanned Systems · Journal of Aerospace Engineering · International Journal of Aerospace Engineering · Aerospace Science and Technology · Journal of Systems and Control Engineering · Drones

**国际会议：** IEEE International Conference on Robotics and Automation (ICRA) · IEEE Conference on Decision and Control (CDC) · IEEE Canadian Conference on Electrical and Computer Engineering (CCECE) · American Control Conference (ACC)

### 担任国际会议评审委员会专家

- The 23rd IEEE International Conference on Industrial Informatics (INDIN 2025) — 会议分项目委员会成员，Track Program Committee (TPC) reviewer (Factory Communications, Control and Automation Systems)
- 2025 IEEE 11th World Forum on Internet of Things (WF-IoT 2025) — 会议分项目委员会成员，Track Program Committee (TPC) reviewer

## 所获奖项

### 公司奖项

| 时间    | 名称                |
| ------- | ------------------- |
| 2023/04 | 华为年度绩效评优A级 |
| 2023/01 | 华为海思质量之星奖  |
| 2021/08 | 华为海思新星奖      |

### 奖学金

| 时间    | 单位                                      | 名称                                                                                                                |
| ------- | ----------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| 2017/02 | University of Toronto（加拿大多伦多大学） | Ontario Trillium Scholarship 加拿大安大略省延龄草奖学金（全安大略省仅75人获得，奖学金共16万加元，约合人民币82万元） |
| 2011/09 | 上海交通大学                              | 上海交通大学三等奖学金                                                                                              |
| 2010/09 | 上海交通大学                              | 上海交通大学三等奖学金                                                                                              |
| 2010/03 | 上海交通大学                              | 上海交通大学三等奖学金                                                                                              |

### 学术贡献奖

| 时间 | 名称                                                                                                                                      |
| ---- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| 2024 | Journal of Guidance, Control, and Dynamics（JGCD）杰出审稿人 Excellent Reviewer for the Journal of Guidance, Control, and Dynamics (JGCD) |
| 2022 | Journal of Guidance, Control, and Dynamics（JGCD）杰出审稿人 Excellent Reviewer for the Journal of Guidance, Control, and Dynamics (JGCD) |
