---
layout: page
title: "Cooperative UWB and LiDAR Drone Navigation with Reinforcement Learning (PPO)"
description: "Observability-Gramian-aware leader–follower formation flight where followers use only an IMU and a single UWB range; LiDAR SLAM for the leader and a PPO planning policy trained in Isaac Lab. Published in JGCD."
lang: en
permalink: /research/uwb-lidar-formation-flight/
category: research
featured: true # shown on the home page
importance: 3
cv_group: utias-postdoc
period: "2025/08 – 2026/03"
---

**Period:** 2025/08 – 2026/03 · University of Toronto Institute for Aerospace Studies

<!-- details -->

- Led a two-person team (1 Ph.D. student, 1 master's student) and proposed a localization and navigation algorithm for drone formation flight based on the observability Gramian (a mathematical tool for measuring whether a system's states can be accurately estimated).
- Unlike conventional formation flight, this method only requires the leader to provide absolute position measurements via GPS or LiDAR SLAM; the followers rely only on their onboard IMU (inertial measurement unit) and a single range measurement from an ultra-wideband (UWB) system to estimate their 3D position relative to the leader, enabling close-proximity formation flight.
- Theoretically analyzed the relationship between the observability Gramian and the follower's localization error, and proposed an optimal leader–follower trajectory planning scheme: the leader and the follower move along specific trajectories so that the follower's Kalman filter can use these trajectories to avoid observability singularities and achieve the minimum estimation error, filling a research gap on this problem. Results were published in the top international aerospace journal, the Journal of Guidance, Control, and Dynamics (JGCD): “Observability-aware control for quadrotor formation flight with range-only measurement” (2026).
- Building on this theoretical scheme, developed a LiDAR-SLAM-based localization solution for the leader, enabling autonomous flight in GPS-denied environments.
- Using Proximal Policy Optimization (PPO) reinforcement learning with the observability Gramian as part of the reward function, built a large-scale parallel reinforcement-learning training framework in NVIDIA Isaac Lab to obtain a reinforcement-learning formation-flight policy. The PPO-generated planning solves the difficulty that the observability-Gramian-based planning problem in the JGCD paper is hard to solve in real time, enabling the practical engineering deployment of this formation-flight scheme.
