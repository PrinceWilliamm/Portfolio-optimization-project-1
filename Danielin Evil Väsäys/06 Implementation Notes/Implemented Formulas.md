---
tags:
  - mathematics
  - python
  - simulation
title: Formulas currently implemented in the program
status: Active
---
Last checked: 2026-07-07.

These formulas are implemented in the external Python project at `K:\Development\Pendulum Simulation Project`.

## Small-Angle Pendulum Model
Used for angular acceleration calculation.
$$
\theta'' = -\frac{g}{L}\theta
$$
## Theoretical Period
Calculates the small-angle theoretical period in seconds
$$
T = 2\pi\sqrt{\frac{L}{g}}
$$
## Time Step sequence

$$
t_i = i\Delta t
$$

$$
0 \leq t_i \leq t_{\text{duration}} + \Delta t
$$
## Angular Acceleration

$$
\alpha_{i-1} = -\frac{g}{L}\theta_{i-1}
$$

## Semi-Implicit Euler Velocity Update

$$
\omega_i = \omega_{i-1} + \alpha_{i-1}\Delta t
$$

**Substituted version**
$$
\omega_i = \omega_{i-1} - \frac{g}{L}\theta_{i-1}\Delta t
$$
## Semi-Implicit Euler Angle Update

$$
\theta_i = \theta_{i-1} + \omega_i\Delta t
$$
## Zero-Crossing Fraction

$$
f = \frac{\theta_{i-1}}{\theta_{i-1} - \theta_i}
$$
## Interpolated Crossing Time

$$
t_{\text{cross}} = t_{i-1} + f(t_i - t_{i-1})
$$

## Simulated Period from Crossings

$$
T_j = t_{\text{cross}, j+1} - t_{\text{cross}, j}
$$

$$
T_{\text{sim}} = \frac{1}{n - 1}\sum_{j=1}^{n-1} T_j
$$

## Elliptic Model Helper

The code also includes a more realistic ideal pendulum helper using elliptic functions. It currently supports zero initial angular velocity.

$$
k = \sin\left(\frac{\theta_0}{2}\right)
$$

$$
K = K(k^2)
$$

$$
\omega = \sqrt{\frac{g}{L}}
$$

The code uses SciPy elliptic functions to calculate the angle over time.

## Energy Helper

The code includes a total mechanical energy helper using mass `m = 1 kg`.

Kinetic energy:

$$
E_k = \frac{1}{2}m(L\omega)^2
$$

Potential energy:

$$
E_p = mgL(1-\cos(\theta))
$$

Total energy:

$$
E_{\text{total}} = E_k + E_p
$$

## Variance Helper

The code can compare two simulation results over their shared time range.

For two angle values at the same time:

$$
\text{variance} = \operatorname{var}(\theta_1, \theta_2)
$$

This is currently used for the Manim animation comparing the small-angle model and elliptic model.

## Variable Labels
$$
\theta = \text{angular displacement}
$$

$$
\omega = \text{angular velocity}
$$

$$
\alpha = \text{angular acceleration}
$$

$$
L = \text{pendulum length}
$$

$$
g = \text{gravitational acceleration}
$$

$$
\Delta t = \text{time step}
$$

$$
T = \text{period}
$$

---
