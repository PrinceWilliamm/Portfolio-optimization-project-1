---
title: "Period Formula"
project: "Pendulum Simulation Project"
status: "Draft"
created: 2026-07-07
---

# Period Formula

## Current status

Last checked: 2026-07-07.

The current Python project implements the small-angle theoretical period formula.

## Formula

```text
T = 2*pi*sqrt(L/g)
```

In mathematical notation:

$$
T = 2\pi\sqrt{\frac{L}{g}}
$$

## Meaning

| Symbol | Meaning |
|---|---|
| `T` | Period of one full oscillation, in seconds |
| `L` | Pendulum length, in meters |
| `g` | Gravitational acceleration, in meters per second squared |

## What the formula predicts

- A longer pendulum has a longer period.
- Stronger gravity gives a shorter period.
- In the ideal small-angle model, mass does not affect the period.

## Connection to the code

The formula is implemented as `theoretical_period(length_m, gravity_m_s2)` in the external Python project.

The length comparison experiment uses this formula to compare theory against the simulated period in [[Pendulum Simulation Project/07 Experiments/Length Comparison|Length Comparison]].

## Limitation

This formula is most accurate for small angles. The current first experiment uses a 5 degree initial angle, so the comparison is appropriate for the minimum viable project.

## Related notes

- [[Pendulum Simulation Project/05 Theory/Key Variables|Key Variables]]
- [[Pendulum Simulation Project/05 Theory/Small-Angle Approximation|Small-Angle Approximation]]
- [[Pendulum Simulation Project/06 Implementation Notes/Implemented Formulas|Implemented Formulas]]
