---
layout: page
title: "基于强化学习（PPO）的UWB和激光雷达无人机协同导航算法研究"
description: "基于可观性Gramian矩阵的长僚机编队定位与导航：僚机仅依赖IMU与单一UWB距离测量；长机激光雷达SLAM定位与Isaac Lab中训练的PPO编队飞行策略。成果发表于JGCD。"
lang: zh-CN
permalink: /zh/projects/uwb-lidar-formation-flight/
category: 科研项目
featured: true # shown on the home page
importance: 3
cv_group: utias-postdoc
period: "2025/08至2026/03"
---

**时间：** 2025/08至2026/03 · 多伦多大学航空航天研究院

<!-- details -->

- 领导两人团队（1博士、1硕士），提出一种基于可观性Gramian矩阵（Observability Gramian，用于衡量系统状态能否被准确估计的数学工具）的无人机编队飞行定位与导航算法。
- 与常规的编队飞行不同，该方法只要求长机（领航机）通过GPS或激光雷达SLAM提供绝对位置测量；僚机仅依赖机载IMU（惯性测量单元）和超宽带系统（Ultra-Wideband，UWB）提供的单一距离测量，即可实现相对于长机的三维位置估计，从而实现近距离编队飞行。
- 该方法从理论上分析了可观性Gramian矩阵与僚机（跟随机）定位误差的关系，提出了一种长机与僚机的最优轨迹规划方案：长机与僚机按特定轨迹运动，使僚机的卡尔曼滤波器能够利用该轨迹规避观测奇异点并获得最小估计误差，填补了该问题的研究空白。成果发表于国际航空顶级期刊Journal of Guidance, Control, and Dynamics（JGCD），参考学术成果：“Observability-aware control for quadrotor formation flight with range-only measurement”（JGCD 2026）。
- 在上述理论方案的基础上，开发基于激光雷达SLAM的长机定位方案，在无GPS的环境下实现自主飞行。
- 利用近端策略优化（Proximal Policy Optimization，PPO）强化学习方法，将可观性Gramian矩阵作为奖励函数的一部分，在NVIDIA Isaac Lab环境中搭建大规模并行强化学习训练框架，实现了强化学习编队飞行策略。PPO生成的规划方案解决了上述JGCD论文中基于可观性Gramian矩阵的规划问题难以实时求解的难题，实现了该编队飞行方案的实际工程落地。
