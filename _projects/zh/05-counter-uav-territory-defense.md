---
layout: page
title: "基于强化学习的无人机区域安全和反无人机拦截算法研究"
description: "仅依赖无线电到达角测量的无人机集群自主防守与拦截：基于MADDPG的主动定位策略与基于RNN的HA-RMAPPO训练框架。成果发表于Science China Technological Sciences。"
lang: zh-CN
permalink: /zh/projects/counter-uav-territory-defense/
category: 科研项目
importance: 5
cv_group: utias-postdoc
period: "2024/09至今"
---

**时间：** 2024/09至今 · 多伦多大学航空航天研究院

<!-- details -->

- 领导三人团队（1硕士、2本科），使用强化学习方法设计无人机自主区域防守拦截算法。该算法仅依赖对入侵无人机的无线电到达角测量，实时规划防守无人机的最优任务分配与飞行轨迹，实现无人机的自主集群防守与拦截。
- 提出一种基于MADDPG（多智能体深度确定性策略梯度）的非法入侵无人机主动定位与位置估计策略。在假设防守无人机搭载小型机载雷达的条件下，训练最优拦截路径，最大化雷达测速与定位精度，提升拦截成功率。参考学术成果：“Investigating Multi-UAV Territory Guarding Using Cooperative-Competitive Reinforcement Learning”（AIAA SciTech 2026）。
- 在上述文献的基础上，提出一种基于HA-RMAPPO的无人机集群区域防御改进强化学习方案，利用入侵无人机的无线电回传信号测量，实现对非法入侵无人机位置的被动滤波与定位。该方案适用于小型低成本无人机集群对入侵无人机的快速定位与拦截。
- 在传统HA-RMAPPO的基础上，提出一种基于RNN的训练框架，相比于MLP架构，在定位拦截问题的训练过程中提升了最终拦截策略的成功率。最终成果发表于中科院1区顶级期刊Science China Technological Sciences：“Hybrid reinforcement learning control for UAV territory guarding with cooperative angle-of-arrival localization”（2026）。
