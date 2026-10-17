---
layout: page
title: "Ph.D. Research: Cooperative Tethered-Payload Transportation with Multiple Drones"
description: "Lyapunov-based nonlinear control for multi-drone tethered-payload transport (JGCD, IEEE TIE, IEEE/ASME TMECH; 300+ citations), implemented from scratch in C++/ROS on a Jetson Nano with a Pixhawk."
lang: en
permalink: /research/phd-cooperative-payload-transport/
category: research
featured: true # shown on the home page
importance: 8
cv_group: utias-phd
period: "2016/09 – 2021/03"
img: assets/img/projects/phd-payload-flight.jpg
card_img: assets/img/projects/phd-payload-card.jpg # home-page card only
---

**Period:** 2016/09 – 2021/03 · Ph.D., University of Toronto Institute for Aerospace Studies · Supervisor: Dr. Hugh H.T. Liu

<div class="row mt-3">
  <div class="col-sm mt-3 mt-md-0">
    {% include youtube.liquid id='ejTnwAZaz20' title='Cooperative tethered-payload transportation with multiple quadrotors' %}
  </div>
</div>
<div class="caption">Flight experiments: cooperative tethered-payload transportation with multiple quadrotors.</div>

<!-- details -->

- Conducted research on the control theory and engineering implementation of autonomous drone transportation systems. For applications in which multiple drones carry a tethered payload, proposed a complete set of nonlinear control methods based on multibody dynamics, achieved cooperative payload transportation with multiple drones, and built an experimental platform to validate the engineering feasibility of the approach, providing a solution to the control challenges of cooperative drone transportation in future smart cities.
- The project was jointly funded by the Natural Sciences and Engineering Research Council of Canada (NSERC) and Drone Delivery Canada, with total funding of C$640,000 (approx. RMB 3.2 million).
- The outstanding doctoral research was supported by full scholarships from the University of Toronto and the Government of Ontario: the Ontario Trillium Scholarship (awarded to only 75 recipients across Ontario), totaling C$160,000 (approx. RMB 820,000).
- On the theoretical side, proposed a nonlinear control system based on the Lyapunov method and proved that it guarantees stable transportation of the tethered payload in the presence of unknown disturbances, providing a technical foundation for safe payload transportation in adverse weather. The results were published in the top international journals Journal of Guidance, Control, and Dynamics (top aerospace journal, CAS JCR Zone 1), IEEE Transactions on Industrial Electronics (top mechatronics and automation journal, CAS Zone 1), and IEEE/ASME Transactions on Mechatronics (top mechatronics and automation journal, CAS Zone 1). The related work has received more than 300 citations and wide recognition in the academic community ([Google Scholar](https://scholar.google.ca/citations?hl=en&user=p2oGLVYAAAAJ)).
- On the engineering side, independently implemented the nonlinear control methods for multi-drone cooperative transportation from scratch. Wrote the flight control programs in C++ and ROS, and implemented the real-time flight control algorithms, as well as command control of the Pixhawk flight control computer, on the resource-constrained NVIDIA Jetson Nano onboard computer, providing a practical software solution for engineering deployment; validated the correctness and fault-tolerant control capability of the proposed methods on quadrotor drones.
- Project video and GitHub repository:
  - YouTube: <https://www.youtube.com/watch?v=ejTnwAZaz20>
  - GitHub: <https://github.com/LonghaoQian/px4_command>

<!-- end details -->

## Theory at a glance

<style>
  mjx-container[display="true"] {
    overflow-x: auto;
    overflow-y: hidden;
    padding: 0.25rem 0;
  }
</style>

The payload, the cables and the quadrotors are modelled and controlled as one multibody system. A hierarchical nonlinear controller with a
disturbance estimator keeps the payload on a reference path, and its stability is proved with the Lyapunov method (JGCD, 2022).

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/phd-system-geometry.jpg" alt="System geometry of the multi-quadrotor slung-payload system" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">System geometry: the quadrotors carry a rigid payload on cables of length l, and the payload follows a piecewise-straight reference path.</div>

**1. One multibody model.** The system splits into a payload subsystem $$\Sigma_p$$ (payload pose, cable directions and all translational
velocities) and one attitude subsystem $$\Sigma_j$$ per quadrotor:

$$
\Sigma_p: \begin{cases} M\dot{u} + C u = G + F + \Delta \\ \dot{x}_p = v_p, \quad \dot{R}_{IP} = R_{IP}\,\omega_p^\times, \quad \dot{r}_j = v_j \end{cases}
\qquad
\Sigma_j: \begin{cases} J\dot{\omega}_j + \omega_j^\times J \omega_j = \tau_j \\ \dot{R}_{Ij} = R_{Ij}\,\omega_j^\times, \quad f_{L,j} = -f_j R_{Ij} e_3 \end{cases}
$$

Here $$u = [\,v_p^\top\ \ \omega_p^\top\ \ v_1^\top \cdots v_N^\top\,]^\top$$ stacks the payload velocity, its angular velocity and the horizontal
cable-tip velocities; $$M$$ and $$C$$ are the inertia and Coriolis matrices; and $$F$$, $$G$$ and $$\Delta$$ are the lift, gravity and disturbance
forces. Each cable vector is $$L_j = [\,r_j^\top,\ -\sqrt{l^2 - r_j^\top r_j}\,]^\top$$, so the horizontal offset $$r_j$$ fully describes it.

**2. Path following.** The payload should slide along segment $$i$$ of the path (start point $$p_i$$, direction $$n_i$$, desired speed
$$v_{d,i}$$) while holding a desired attitude $$R_{IP,d}$$:

$$
e_{p,i} = (I - n_i n_i^\top)(x_p - p_i), \qquad e_{v,i} = v_p - v_{d,i}, \qquad e_r = \tfrac{1}{2}\big(R_{PI,d} R_{IP} - R_{PI} R_{IP,d}\big)^\vee .
$$

The goal is to make the zero error state asymptotically stable. At least three quadrotors are needed: weights $$a_j > 0$$ with
$$\sum_j a_j t_j = 0$$, $$\sum_j a_j = 1$$ and $$\operatorname{rank}\big(\sum_j a_j t_j^\times t_j^\times\big) = 3$$ let the lift be shared without
adding a net moment on the payload.

**3. A hierarchical controller.** The outer loop is a virtual control law that computes the lift vector each quadrotor should produce. The inner loop
is an attitude tracker on each quadrotor that tilts it to produce that lift.

<div class="row">
  <div class="col-sm-10 mx-auto mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/phd-control-diagram.png" alt="Control diagram of the system" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
  Control diagram: the virtual control law gives each quadrotor's lift vector, from which a thrust and a target attitude are extracted for the attitude
  controller.
</div>

With the sliding variables $$s_p = e_{v,i} + k_v e_{p,i}$$ and $$s_r = \omega_p + k_r e_r$$, the virtual force of quadrotor $$j$$ is

$$
f_{v,j} = \hat{f}_{t,j} + \hat{f}_{0,j} + f_{a,j} + f_{b,j} + f_{c,j}, \qquad
f_{b,j} = -a_j\big(m_p \hat{\xi} + k_p m_p s_p\big), \qquad
f_{c,j} = -a_j R_{IP} E_j \big(J_p \hat{\eta} + k_\Omega s_r\big),
$$

where $$\hat{f}_{t,j}$$ is a trimming force that balances the weight and the estimated disturbances, $$\hat{f}_{0,j}$$ synchronizes the quadrotor with
the payload, and $$f_{a,j}$$, $$f_{b,j}$$ and $$f_{c,j}$$ remove the path-following error. Each quadrotor then flies with thrust
$$f_j = \lVert f_{v,j} \rVert$$, and an almost globally asymptotically stable attitude tracker follows the attitude extracted from $$f_{v,j}$$.

**4. Disturbance estimation (UDE).** Wind and model errors are estimated from the mismatch between each quadrotor's measured acceleration and the
modelled forces, passed through a low-pass filter:

$$
\hat{\Delta}_j = \int_0^t \kappa_j\, \mathfrak{B}_j \big( m_j \dot{v}_{q,j} - f_{L,j} - m_j g_I - \hat{\Delta}_j \big)\, d\tau, \qquad
\hat{\Delta}_{\perp,j} = \Big(I - \frac{L_j L_j^\top}{l^2}\Big)\hat{\Delta}_j .
$$

Similar laws give the effective force $$\hat{\Delta}_T$$ and torque $$\hat{\Delta}_R$$ on the payload. Their integral terms accumulate the
path-following error, so the estimator acts like a nonlinear PID controller with guaranteed stability.

**5. Stability.** The Lyapunov function combines the kinetic energy of the error motion, a cable-angle penalty, the path and attitude errors, and the
estimation errors:

$$
V = V_1 + \sum_{j=1}^{N} a_j V_{2,j} + V_3 + V_4, \qquad
V_1 = \tfrac{1}{2}(u + u_d)^\top M (u + u_d), \qquad
V_3 = k_p k_v m_p\, e_{p,i}^2 + k_r k_\Omega \operatorname{tr}\big(I - R_{PI,d}^\top R_{PI}\big).
$$

Its derivative is bounded by a quadratic form,

$$
\dot{V} \le -\sum_{j=1}^{N} a_j\, u_K^\top \begin{bmatrix} H_{K,j} & H_{K,\Delta} \\ H_{K,\Delta}^\top & H_{\Delta,j} \end{bmatrix} u_K \le 0 ,
$$

which holds when the gains make $$H_{K,j}$$ positive definite. LaSalle's theorem then gives asymptotic stability of the outer loop. Because the
attitude tracker is almost globally asymptotically stable, a reduction theorem extends this to the complete system inside an estimated domain of
attraction (Theorem 1 of the paper).

## Flight experiments

The controller was flown in the FSC OptiTrack lab with three S500 quadrotors. Fourteen OptiTrack cameras measured the poses of the quadrotors and the
payload, and an NVIDIA Jetson Nano on each quadrotor received this feedback at 50 Hz over 5 GHz Wi-Fi. In the test below, an extra object is placed
on the payload platform, so the payload no longer matches its model.

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/phd-added-mass-test.jpg" alt="Flight test with an additional object on the payload" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
  Flight test with an additional object on the payload platform. (a) The test. (b) Payload position for a step in x from −0.3 m to 0.6 m (I), and
  payload attitude for a yaw step from −20° to 20° (II). Both converge to the commands without steady-state error.
</div>

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/phd-estimated-disturbances.png" alt="Estimated disturbances during the flight test" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
  Estimated disturbances in the same test. (a) Effective force and torque on the payload: the vertical force drifts as the battery drains, and the
  high-frequency part comes from air turbulence and structural flexibility. (b) Estimated disturbances on each quadrotor, mainly caused by airframe
  deformation.
</div>
