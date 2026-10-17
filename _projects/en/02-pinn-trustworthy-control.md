---
layout: page
title: "Trustworthy AI Control Framework Based on Physics-Informed Neural Networks (PINNs)"
description: "PINN-trained controllers with stability guarantees, generated without any training data; contraction metrics on Riemannian manifolds (RCCM) for singularity-free robust control. Accepted at CDC 2026 and AIAA SciTech 2027."
lang: en
permalink: /research/pinn-trustworthy-control/
category: research
featured: true # shown on the home page
importance: 2
cv_group: utias-postdoc
period: "2025/08 – 2026/03"
img: assets/img/projects/ccm-payload-gate-thumb.jpg
card_img: assets/img/projects/ccm-training-framework.png # home-page card only
card_video: assets/video/ccm-payload-gate-sim-card.mp4 # home-page card only
card_video_poster: assets/img/projects/ccm-payload-gate-sim-card-poster.jpg
---

**Period:** 2025/08 – 2026/03 · University of Toronto Institute for Aerospace Studies

<div class="row mt-3">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/ccm-training-framework.png" alt="Training framework for the neural CCM and the neural feedback controller" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
    <figure>
      <video
        src="{{ 'assets/video/ccm-payload-gate-sim.mp4' | relative_url }}"
        poster="{{ 'assets/img/projects/ccm-payload-gate-sim-poster.jpg' | relative_url }}"
        class="img-fluid rounded z-depth-1"
        autoplay
        loop
        muted
        playsinline
      ></video>
    </figure>
  </div>
</div>
<div class="caption">
  Left: the neural dual CCM and the neural feedback controller are trained jointly from the system dynamics. Right: simulation of three drones carrying a
  rigid-body payload on variable-length cables through a gate under the learned contraction controller.
</div>

<!-- details -->

- Led a two-person team (1 Ph.D. student, 1 master's student) and proposed a nonlinear control training method based on physics-informed neural networks (PINNs) that enables neural networks to automatically generate robust control algorithms from a system's multibody dynamics equations without any training dataset, enabling rapid generation of control schemes for complex systems. Compared with conventional machine-learning control, the PINN-generated controllers strictly satisfy the theoretical requirements of control stability, yielding reliable neural-network-based control.
- Through differential geometry, combined PINNs with Riemannian manifold theory to achieve singularity-free control of the spatial attitude of drones and robots. Combined with contraction analysis control theory, transformed the robust control problem into the solution of a partial differential equation (PDE), and then solved the PDE with PINNs to obtain control networks with stability guarantees.
- Proposed, for the first time, a robust control theory combining PINNs with Riemannian manifolds (Robust Control Contraction Metrics, RCCM), which still guarantees control accuracy in the presence of unknown external disturbances and parameter uncertainties.
- The PINN-based AI control framework proposed in this research can be widely applied to the control of unmanned systems and embodied intelligence.
- Results have been accepted by the top international control conference, the IEEE Conference on Decision and Control (CDC 2026), and by the AIAA 2027 SciTech Forum: “Neural Robust Control on Lie Groups Using Contraction Methods” (CDC 2026) and “Contraction-based Neural Control for Cooperative Aerial Payload Transportation with Variable-length Cables” (AIAA SciTech 2027).

<!-- end details -->

## Theory at a glance

<style>
  mjx-container[display="true"] {
    overflow-x: auto;
    overflow-y: hidden;
    padding: 0.25rem 0;
  }
</style>

Both papers turn stability into conditions on a Riemannian metric, then let neural networks find a metric and a controller that satisfy those conditions
at sampled states. No demonstration data is needed, only the system's equations of motion.

### Background

**A. Contraction analysis: what it is.** Lyapunov analysis asks whether trajectories converge to one equilibrium. Contraction analysis
(Lohmiller and Slotine, 1998) asks a stronger question: do _any two_ neighbouring trajectories converge to each other? It looks at the differential
(virtual) dynamics $$\delta\dot{x} = A(x)\,\delta x$$ with $$A = \partial f / \partial x$$, and measures the length of $$\delta x$$ with a
Riemannian metric $$M(x) \succ 0$$. If that length shrinks at a uniform rate $$\lambda$$,

$$
\frac{d}{dt}\big(\delta x^\top M(x)\,\delta x\big) \le -2\lambda\, \delta x^\top M(x)\,\delta x
\quad \Longleftrightarrow \quad
\dot{M} + \langle M A \rangle + 2\lambda M \preceq 0 ,
$$

then all trajectories converge to each other exponentially. With $$\underline{m} I \preceq M \preceq \overline{m} I$$,

$$
\lVert x_1(t) - x_2(t) \rVert \le \sqrt{\overline{m}/\underline{m}}\; e^{-\lambda t}\, \lVert x_1(0) - x_2(0) \rVert .
$$

**Why use it for control.**

- _Tracking, not just stabilization._ If all trajectories converge to each other, the system converges to whichever feasible reference
  $$(x^*, u^*)$$ the planner sends. There is no need to build a new Lyapunov function for every trajectory.
- _Pointwise conditions._ The certificate is a matrix inequality at each state $$x$$. It can be checked, or penalized in a loss, one sampled state at a
  time, which is exactly what neural-network training needs.
- _Robustness with numbers._ Disturbances enter the differential dynamics as an extra input, which gives explicit gain bounds and error tubes rather
  than a qualitative "it is stable".

**B. Control contraction metrics (CCM).** Manchester and Slotine (2017) extended contraction to systems with inputs,
$$\dot{x} = f(x) + B(x)u$$. A CCM is a metric for which some differential feedback $$\delta u = K(x)\,\delta x$$ makes the closed loop contract,
$$\dot{M} + \langle M(A + BK) \rangle + 2\lambda M \preceq 0$$. With the dual metric $$W = M^{-1}$$ and $$B_\perp$$ spanning the directions the inputs
cannot reach ($$B_\perp^\top B = 0$$), sufficient conditions that no longer depend on $$u$$ are

$$
B_\perp^\top \Big( -\partial_f W + \big\langle \tfrac{\partial f}{\partial x} W \big\rangle + 2\lambda W \Big) B_\perp \prec 0,
\qquad
\partial_{b_i} W - \big\langle \tfrac{\partial b_i}{\partial x} W \big\rangle = 0 .
$$

The first says the system must contract on its own in the directions the controller cannot push. The second says the metric does not change along
the input directions (the $$b_i$$ are Killing fields), so the controller can make those directions contract. If such a metric exists, a controller that
tracks any feasible trajectory exists too. The robust version (RCCM; Manchester and Slotine, 2018) adds the disturbance input and turns contraction into
the $$\mathcal{L}_\infty$$ gain bound used below.

**C. Lie groups.** A Lie group is a smooth manifold that is also a group. The attitude of a drone, a payload or a robot link is a rotation,

$$
SO(3) = \{\, R \in \mathbb{R}^{3\times 3} : R^\top R = I_3,\ \det R = 1 \,\},
\qquad
\dot{R} = R\, \omega^\wedge ,
$$

where $$\omega^\wedge$$ is the skew-symmetric matrix of the angular velocity $$\omega$$. Coordinates such as Euler angles break down: they are singular at
$$\pm 90^\circ$$ pitch (gimbal lock) and distort distances, and quaternions cover each rotation twice. Working on the group itself is globally valid.
Every Lie group is _parallelizable_: the velocity at any $$R$$ is $$R\,\xi^\wedge$$ for some $$\xi \in \mathbb{R}^3$$, so a single smooth basis
$$S(x)$$ spans the tangent space everywhere, and every tangent vector can be written as $$\delta x = S(x)\,v$$ with intrinsic coordinates
$$v$$.

**D. Why CCM needs the Lie-group view.** CCM theory is written for $$\mathbb{R}^n$$. A rotation stored as the 9 entries of $$R$$ has only 3 degrees
of freedom, so a Euclidean metric on $$\mathbb{R}^9$$ would also have to contract in 6 directions that leave $$SO(3)$$ and have no physical meaning.
The papers below instead write the differential dynamics in the intrinsic coordinates $$v$$ and search for a smaller metric $$\mathcal{M}(x)$$ on the
tangent space only, lifted back with the projection $$P_S = S(S^\top S)^{-1}$$:

$$
\delta x = S\,v, \qquad B = S\,E, \qquad B_w = S\,E_w, \qquad M(x) = P_S(x)\, \mathcal{M}(x)\, P_S(x)^\top .
$$

As a result, the certificate is valid for every attitude with no singularities. Errors are measured as distances on the manifold, using the
Lie-algebra error $$\varepsilon_r = \tfrac{1}{2}\big(R^{*\top} R - R^\top R^*\big)^\vee$$ for rotations. The matrix conditions also shrink: for the
three-drone payload the state is a 24-dimensional manifold embedded in $$\mathbb{R}^{30}$$, so the networks learn $$24\times 24$$ metrics instead of
$$30\times 30$$ ones.

### Results

**1. Systems on Lie groups.** The state lives on a manifold $$\mathcal{X}$$ (for a quadrotor, $$\mathbb{R}^3 \times SO(3)$$ and its velocities), with
disturbance $$w$$, output $$z$$ and a feedback law around a reference $$(x^*, u^*)$$:

$$
\dot{x} = f(x) + B(x)\,u + B_w(x)\,w, \qquad z = g(x,u), \qquad u = k(x,x^*) + u^* .
$$

As in D, differential lengths are measured on the tangent space, $$V = v^\top \mathcal{M}(x)\, v$$ with $$\delta x = S(x)\,v$$.

**2. Robust control contraction metric (RCCM).** The closed loop has an $$\mathcal{L}_\infty$$ gain $$\alpha$$ from disturbance to output if there are a
uniformly bounded metric $$\mathcal{M}(x)$$ and constants $$\lambda, \mu > 0$$ such that

$$
R_1 = \begin{bmatrix} \dot{\mathcal{M}} + \langle \mathcal{M}\mathcal{A} \rangle + 2\lambda\mathcal{M} & \mathcal{M}E_w \\ E_w^\top \mathcal{M} & -\mu I_p \end{bmatrix} \preceq 0,
\qquad
R_2 = \begin{bmatrix} 2\lambda\mathcal{M} - \alpha^{-1}\mathcal{C}^\top\mathcal{C} & 0 \\ 0 & (\alpha-\mu) I_p \end{bmatrix} \succeq 0,
$$

where $$\mathcal{A}$$ and $$\mathcal{C}$$ are the closed-loop differential dynamics and output map in intrinsic coordinates.

**3. What it guarantees.** The tracking error is bounded by the size of the disturbance,

$$
\lVert z - z^* \rVert^2_{\mathcal{L}_\infty^{[0,T]}} \le \alpha^2 \, \lVert w - w^* \rVert^2_{\mathcal{L}_\infty^{[0,T]}} + \beta\big(x(0), x^*(0)\big),
$$

so after transients the output stays inside a tube $$\Omega(z^*) = \{\, y : \lVert y - z^* \rVert \le \alpha \bar{w} \,\}$$ around the reference.

**4. Learning the certificate.** The controller and the dual metric $$\mathcal{W} = \mathcal{M}^{-1}$$ are neural networks, built so that
$$k_{nn}(x,x) = 0$$ and $$\mathcal{W} \succeq \overline{m}^{-1} I$$ hold by construction:

$$
k_{nn}(x,x^*) = K_1(x,x^*;\theta_{k_1}) \tanh\!\big(K_2(x,x^*;\theta_{k_2})\, \varepsilon(x,x^*)\big), \qquad
\mathcal{W}(x) = \Theta(x;\theta_w)^\top \Theta(x;\theta_w) + \overline{m}^{-1} I .
$$

They are trained jointly on states sampled from the operating region, with a loss that penalizes every violation of the conditions:

$$
\mathcal{L}_k = \mathrm{L_{PD}}(-R_1) + \mathrm{L_{PD}}(R_2) + \mathrm{L_{PD}}(-C_1) + \sum_i \lVert C_{2,i} \rVert_F + \sum_j \lVert C_{3,j} \rVert_F
+ \mathrm{L_{PD}}(\underline{m}^{-1} I - \mathcal{W}) + \mathrm{ReLU}(\alpha - \underline{\alpha}),
$$

where $$\mathrm{L_{PD}}$$ penalizes a matrix that is not positive semidefinite, $$C_1$$ asks the uncontrolled system to contract in directions the
inputs cannot reach, and $$C_{2,i}, C_{3,j}$$ make the input and disturbance directions Killing fields of the metric (CDC 2026).

<div class="row">
  <div class="col-sm-8 mx-auto mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/ccm-trajectory-comparison.png" alt="Trajectory tracking comparison" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
  Simulated quadrotor trajectory tracking from the same initial position: reference, geometric controller, CCM, RCCM, and RCCM with UDE.
</div>

**5. Application: cooperative payload transport with variable-length cables (AIAA SciTech 2027).** For three drones carrying a rigid-body payload, the
equations of motion are arranged so that the payload and the cable lengths are driven by separate control channels. The payload subsystem
$$\Sigma_p$$ (state in $$\mathbb{R}^{21} \times SO(3)$$) gets a neural CCM controller that enforces

$$
C_{CCM} = \dot{\mathcal{M}} + \langle \mathcal{M}\mathcal{A} \rangle + 2\lambda\mathcal{M} \preceq 0,
$$

while the cable-length subsystem is a simple double integrator with its own tracker,

$$
\Sigma_l: \quad \frac{d}{dt}\begin{bmatrix} l \\ \dot{l} \end{bmatrix} = \begin{bmatrix} \dot{l} \\ 0 \end{bmatrix} + \begin{bmatrix} 0 \\ I_N \end{bmatrix} \tilde{f}_{\parallel},
$$

so the formation can shorten its cables to fly through height-constrained gates, as in the simulation above.

<div class="row">
  <div class="col-sm-8 mx-auto mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/ccm-payload-geometry.png" alt="Geometry of the multi-drone variable-length cable payload system" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">System geometry: quadrotors, variable-length cables on pulleys, and the rigid-body payload.</div>
