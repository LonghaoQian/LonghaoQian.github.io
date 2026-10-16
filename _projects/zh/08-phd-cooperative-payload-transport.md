---
layout: page
title: "博士研究：多无人机协同绳系负载运输的控制理论与工程实现"
description: "基于多体动力学与李雅普诺夫方法的多无人机协同绳系负载运输非线性控制（JGCD、IEEE TIE、IEEE/ASME TMECH，引用超过300次），基于C++与ROS在Jetson Nano及Pixhawk上从零实现。"
lang: zh-CN
permalink: /zh/projects/phd-cooperative-payload-transport/
category: 科研项目
importance: 8
cv_group: utias-phd
period: "2016/09至2021/03"
---

**时间：** 2016/09至2021/03 · 博士，多伦多大学航空航天研究院 · 导师：Dr. Hugh H.T. Liu（刘洪涛教授）

<!-- details -->

- 从事无人机自主运输系统的控制理论与工程实现研究。针对多无人机绳系负载的应用场景，提出了一整套基于多体动力学的非线性控制方法，实现了多无人机协同负载运输，并搭建实验平台验证了方案的工程可行性，为未来智慧城市中无人机协同运输的控制难题提供了解决方案。
- 该项目由加拿大自然科学与工程研究理事会（Natural Sciences and Engineering Research Council of Canada，NSERC）和Drone Delivery Canada公司共同资助，项目总金额为64万加元（约320万人民币）。
- 博士期间的杰出研究获得加拿大多伦多大学和安大略省政府全额奖学金：Ontario Trillium Scholarship（加拿大安大略省延龄草奖学金，全安大略省仅75人获得），奖学金共16万加元，约合人民币82万元。
- 在理论研究方面，提出了一套基于李雅普诺夫方法的非线性控制系统，并证明其在存在未知干扰的情况下能够保证绳系负载的稳定运输，为后续在恶劣天气下的负载安全运输提供了技术基础。学术成果发表于国际顶级期刊Journal of Guidance, Control, and Dynamics（航空类顶级期刊，中科院JCR 1区顶级期刊）、IEEE Transactions on Industrial Electronics（机电自动化顶级期刊，中科院1区顶级期刊）和IEEE/ASME Transactions on Mechatronics（机电自动化顶级期刊，中科院1区顶级期刊）。目前相关工作已获得超过300次学术引用，得到了学术界的广泛认可（可参考[谷歌学术](https://scholar.google.ca/citations?hl=en&user=p2oGLVYAAAAJ)）。
- 在工程实现方面，从零开始自主实现了多无人机协同运输的非线性控制方法。使用C++和ROS编写飞行控制程序，在资源有限的机载电脑NVIDIA Jetson Nano上实现了实时飞行控制算法以及对Pixhawk飞控计算机的指令控制，为方法的工程落地提供了切实可用的软件方案，并在四旋翼无人机上验证了所提方法的正确性与容错控制能力。
- 项目视频和GitHub网站如下：
  - YouTube：<https://www.youtube.com/watch?v=ejTnwAZaz20>
  - GitHub：<https://github.com/LonghaoQian/px4_command>
