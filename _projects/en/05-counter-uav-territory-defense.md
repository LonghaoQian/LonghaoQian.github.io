---
layout: page
title: "Reinforcement Learning for Drone Territory Security and Counter-UAV Interception"
description: "Autonomous swarm defense and interception from radio angle-of-arrival measurements alone, using MADDPG and an RNN-based HA-RMAPPO framework. Published in Science China Technological Sciences."
lang: en
permalink: /research/counter-uav-territory-defense/
category: research
featured: true # shown on the home page
importance: 5
cv_group: utias-postdoc
period: "2024/09 – present"
img: assets/img/projects/cuas-thumb.jpg
card_img: assets/img/projects/cuas-card.jpg # home-page card only
---

**Period:** 2024/09 – present · University of Toronto Institute for Aerospace Studies

<div class="row mt-3">
  <div class="col-sm-8 mt-3 mt-md-0 d-flex align-items-center">
    {% include figure.liquid path="assets/img/projects/cuas-ctde-framework.png" alt="HA-RMAPPO centralized training with decentralized execution" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/cuas-rollout-7v3-aoa20.png" alt="Seven defenders against three intruders under AoA noise" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
  Left: HA-RMAPPO with centralized training and decentralized execution. Each defender has its own actor network (MLP encoder, GRU, MLP heads), a
  centralized critic guides training, and rollouts come from parallel environments. Right: a Phase II rollout with seven defenders (green) and three
  intruders (blue) under the heaviest angle-of-arrival noise tested, σ₀ = 20°. The grey ellipses are the 3σ position beliefs; this run ends in a breach.
</div>

<!-- details -->

- Led a three-person team (1 master's student, 2 undergraduates) to design autonomous territory-defense interception algorithms for drones using reinforcement learning. Relying only on radio angle-of-arrival measurements of intruding drones, the algorithm plans the optimal task allocation and flight trajectories of the defending drones in real time, achieving autonomous swarm defense and interception.
- Proposed an active localization and position-estimation strategy for illegally intruding drones based on MADDPG (Multi-Agent Deep Deterministic Policy Gradient). Assuming that the defending drones carry small onboard radars, trained optimal interception paths that maximize radar velocity-measurement and localization accuracy, improving the interception success rate. See “Investigating Multi-UAV Territory Guarding Using Cooperative-Competitive Reinforcement Learning” (AIAA SciTech 2026).
- Building on that work, proposed an improved HA-RMAPPO-based reinforcement-learning scheme for drone-swarm territory defense, which uses measurements of the intruding drone's radio return signals to achieve passive filtering and localization of illegally intruding drones. The scheme is suitable for rapid localization and interception of intruding drones by swarms of small, low-cost drones.
- Building on conventional HA-RMAPPO, proposed an RNN-based training framework that, compared with an MLP architecture, improves the success rate of the final interception policy during training on the localization-and-interception problem. The final results were published in Science China Technological Sciences, a CAS Zone 1 top journal: “Hybrid reinforcement learning control for UAV territory guarding with cooperative angle-of-arrival localization” (2026).

<!-- end details -->

## The challenge

- **Many agents, partial information.** A swarm of defender drones must protect a zone against agile first-person-view (FPV) intruders. The
  defenders sense the intruders only through passive radio angle-of-arrival (AoA) bearings, without range, so the planning policy has to act on
  partial and noisy information.
- **Coordination is hard to design by hand.** Deciding in real time which defender localizes and which intercepts each intruder is a hard
  cooperative planning problem.

## Swarm intelligence with RL

Reinforcement learning works as a generator of planning schemes: once trained, the policy produces decisions in real time, and it can cope with
partial information and cluttered environments. The HA-RMAPPO framework (Science China Technological Sciences, 2026) has five parts:

- **Belief from bearings.** A centralized particle filter (CPF) fuses the AoA bearings, whose noise grows with range, into a belief over each
  intruder's position with a 3σ confidence ellipse.
- **Hybrid action.** Each defender outputs a discrete assignment (which intruder to sense or intercept) and a continuous planar velocity command.
- **Threat-triggered switching.** A probabilistic threat score, based on the earliest time a confidence ellipse would reach the protected zone,
  switches the team from reducing uncertainty to rapid interception.
- **Recurrent CTDE training.** GRU-based actors and a centralized critic are trained with PPO under centralized training and decentralized execution,
  for 10⁷ environment steps across 128 parallel environments.
- **Two-phase curriculum.** Phase I learns coordination with ground-truth intruder states. Phase II fine-tunes on the CPF beliefs under partial
  observability.

## Results

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/cuas-rollouts-2v1.png" alt="HA-RMAPPO rollouts with two defenders and one intruder" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
  Two defenders against one intruder. (a) Phase I, trained with ground-truth states. (b) Phase II, acting on the CPF belief built from AoA bearings
  (grey: confidence ellipse), with threat assessment and stage switching.
</div>

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/cuas-comparison-7v3.png" alt="Training comparison of HA-RMAPPO, MAPPO and IPPO" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
  Seven defenders against three intruders, Phase II training: (a) defense success rate and (b) mean log-determinant of the belief covariance, for
  HA-RMAPPO, MAPPO and IPPO.
</div>

Final defense success rate after 10⁷ training steps (Phase II, averaged over the last 100 episodes):

| Defenders v intruders | HA-RMAPPO (ours) | MAPPO | IPPO  |
| --------------------- | ---------------- | ----- | ----- |
| 2v1                   | **0.703**        | 0.121 | 0.232 |
| 5v2                   | **0.911**        | 0.608 | 0.648 |
| 7v3                   | **0.770**        | 0.185 | 0.081 |
