---
layout: page
title: "基于强化学习和物理信息神经网络的空中吊运操作机器人控制算法研究"
description: "六人团队：基于PINN与鲁棒干扰观测器的容错控制、PPO Sim2Real控制校正、Jetson Orin神经网络部署，以及基于CubeMars AK40-10关节电机与CAN通信的实时缆绳操纵系统。"
lang: zh-CN
permalink: /zh/research/aerial-slung-load-manipulation/
category: 科研项目
importance: 4
cv_group: utias-postdoc
period: "2025/04至2026/06"
---

**时间：** 2025/04至2026/06 · 多伦多大学航空航天研究院

<!-- details -->

- 领导六人团队（3博士、2硕士、1本科），研究基于强化学习和物理信息神经网络的空中吊运操作机器人建模、飞行控制与轨迹规划算法。
- 提出一种基于物理信息神经网络（Physics-Informed Neural Networks，PINNs）的非线性控制训练框架，依据自动控制的稳定性原理自主训练出具有容错能力的控制算法，并结合鲁棒干扰观测器原理，首次实现了强外界干扰下空中吊运操作机器人的多机协同控制。
- 采用近端策略优化（Proximal Policy Optimization，PPO）强化学习方法结合域随机化（Domain Randomization），缩小Sim2Real（仿真到真实环境迁移）差距。在NVIDIA Isaac Sim中训练PPO控制校正算法，减小了由实际系统推力不稳定、建模偏差和气流干扰造成的操作误差。
- 结合PINNs与PPO控制方法，基于C++和PyTorch在NVIDIA Jetson Orin机载电脑上部署神经网络，首次在无人机系统上实现基于PINNs的空中吊运操作机器人多机协同控制。
- 实现了基于CubeMars AK40-10关节电机和CAN通信系统的实时负载缆绳操纵系统，并在四旋翼飞行平台上验证了所提出的控制算法。
- 目前成果正在审稿中，参考学术成果：“A Robust Neural Control Design for Multi-drone Slung Payload Manipulation with Control Contraction Metrics”（arXiv:2510.01489）、“Robust Anti-windup Tracking Control For A Pair of Quadrotors Carrying A Rigid-body Payload With Variable-Length Cable”（Automatica）、“Robust Neural Contraction Slung Load Manipulation With Active Cable Length Control”（JGCD）。
