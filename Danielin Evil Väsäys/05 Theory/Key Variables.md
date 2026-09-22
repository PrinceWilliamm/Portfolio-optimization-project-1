---
title: "Key Variables"
project: "Pendulum Simulation Project"
status: "Draft"
created: 2026-07-07
---

# Key Variables

## Current status

Last checked: 2026-07-07.

These are the main variables used in the current Python implementation.

## Variables

| Symbol / name | Meaning | Unit | Used in code as |
|---|---|---:|---|
| `L` | Pendulum length | m | `length_m` |
| `g` | Gravitational acceleration | m/s^2 | `gravity_m_s2` |
| `theta` | Angular displacement from equilibrium | radians | `angle_rad` |
| `theta_0` | Initial angle | radians | `initial_angle_rad` |
| `omega` | Angular velocity | rad/s | `angular_velocity_rad_s` |
| `dt` | Time step | s | `time_step_s` |
| `T` | Period of one full oscillation | s | `theoretical_period`, `estimate_period` |

## First experiment values

For [[Pendulum Simulation Project/07 Experiments/Length Comparison|Length Comparison]]:

- Gravity: `9.81 m/s^2`
- Initial angle: `5 degrees`
- Time step: `0.005 s`
- Duration: `12.0 s`
- Tested lengths: `0.25 m`, `0.5 m`, `1.0 m`, `1.5 m`, `2.0 m`

## Important note

The code stores angles in radians. Degrees are easier to read, but radians are better for the formulas and Python math functions.

## Related notes

- [[Pendulum Simulation Project/05 Theory/Period Formula|Period Formula]]
- [[Pendulum Simulation Project/06 Implementation Notes/Simulation Plan|Simulation Plan]]
- [[Pendulum Simulation Project/06 Implementation Notes/Python Function Notes|Python Function Notes]]
