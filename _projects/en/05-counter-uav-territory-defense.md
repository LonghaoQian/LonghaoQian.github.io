---
layout: page
title: "Reinforcement Learning for Drone Territory Security and Counter-UAV Interception"
description: "Autonomous swarm defense and interception from radio angle-of-arrival measurements alone, using MADDPG and an RNN-based HA-RMAPPO framework. Published in Science China Technological Sciences."
lang: en
permalink: /research/counter-uav-territory-defense/
category: research
importance: 5
cv_group: utias-postdoc
period: "2024/09 – present"
---

**Period:** 2024/09 – present · University of Toronto Institute for Aerospace Studies

<!-- details -->

- Led a three-person team (1 master's student, 2 undergraduates) to design autonomous territory-defense interception algorithms for drones using reinforcement learning. Relying only on radio angle-of-arrival measurements of intruding drones, the algorithm plans the optimal task allocation and flight trajectories of the defending drones in real time, achieving autonomous swarm defense and interception.
- Proposed an active localization and position-estimation strategy for illegally intruding drones based on MADDPG (Multi-Agent Deep Deterministic Policy Gradient). Assuming that the defending drones carry small onboard radars, trained optimal interception paths that maximize radar velocity-measurement and localization accuracy, improving the interception success rate. See “Investigating Multi-UAV Territory Guarding Using Cooperative-Competitive Reinforcement Learning” (AIAA SciTech 2026).
- Building on that work, proposed an improved HA-RMAPPO-based reinforcement-learning scheme for drone-swarm territory defense, which uses measurements of the intruding drone's radio return signals to achieve passive filtering and localization of illegally intruding drones. The scheme is suitable for rapid localization and interception of intruding drones by swarms of small, low-cost drones.
- Building on conventional HA-RMAPPO, proposed an RNN-based training framework that, compared with an MLP architecture, improves the success rate of the final interception policy during training on the localization-and-interception problem. The final results were published in Science China Technological Sciences, a CAS Zone 1 top journal: “Hybrid reinforcement learning control for UAV territory guarding with cooperative angle-of-arrival localization” (2026).
