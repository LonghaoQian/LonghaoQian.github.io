---
layout: page
title: "Control of Aerial Slung-Load Manipulation Robots with Reinforcement Learning and Physics-Informed Neural Networks"
description: "Six-person team: PINN-trained fault-tolerant control with robust disturbance observers, PPO sim-to-real correction, Jetson Orin deployment, and a real-time cable-manipulation system built on CubeMars AK40-10 motors and CAN."
lang: en
permalink: /research/aerial-slung-load-manipulation/
category: research
importance: 4
cv_group: utias-postdoc
period: "2025/04 – 2026/06"
---

**Period:** 2025/04 – 2026/06 · University of Toronto Institute for Aerospace Studies

<!-- details -->

- Led a six-person team (3 Ph.D. students, 2 master's students, 1 undergraduate) researching modeling, flight control, and trajectory planning algorithms for aerial slung-load manipulation robots based on reinforcement learning and physics-informed neural networks.
- Proposed a nonlinear control training framework based on physics-informed neural networks (PINNs) that autonomously trains fault-tolerant control algorithms according to the stability principles of automatic control and, combined with the principle of robust disturbance observers, achieved for the first time multi-drone cooperative control of aerial slung-load manipulation robots under strong external disturbances.
- Used Proximal Policy Optimization (PPO) reinforcement learning combined with domain randomization to narrow the Sim2Real (simulation-to-reality transfer) gap. Trained a PPO control-correction algorithm in NVIDIA Isaac Sim, reducing the manipulation errors caused by thrust instability, modeling errors, and airflow disturbances in the real system.
- Combining PINNs with PPO control, deployed the neural networks on an NVIDIA Jetson Orin onboard computer using C++ and PyTorch, achieving for the first time PINN-based multi-drone cooperative control of aerial slung-load manipulation robots on a drone system.
- Implemented a real-time payload-cable manipulation system based on CubeMars AK40-10 joint motors and a CAN communication system, and validated the proposed control algorithms on a quadrotor flight platform.
- The results are currently under review: “A Robust Neural Control Design for Multi-drone Slung Payload Manipulation with Control Contraction Metrics” (arXiv:2510.01489), “Robust Anti-windup Tracking Control For A Pair of Quadrotors Carrying A Rigid-body Payload With Variable-Length Cable” (Automatica), and “Robust Neural Contraction Slung Load Manipulation With Active Cable Length Control” (JGCD).
