---
title: "Numerical Method Notes"
project: "Pendulum Simulation Project"
status: "Implemented"
created: 2026-07-07
---

# Numerical Method Notes

## Goal

Choose a method that is simple enough for beginners but accurate enough for the first project.

## Current decision

Last checked: 2026-07-07.

The implemented first method is **Option B - step-by-step numerical update**, using the semi-implicit Euler method.

The code is in:

```text
K:\Development\Pendulum Simulation Project\src\pendulum_simulation\simulation.py
```

The method updates:

1. angular acceleration from the current angle,
2. angular velocity from angular acceleration,
3. angle from the updated angular velocity.

This is more like a real simulation than directly using the cosine solution.

## Option A - Small-angle formula for angle over time

For the first graph, the simulation can use the small-angle solution:

```text
theta(t) = theta_0 * cos(sqrt(g/L) * t)
```

Pros:

- Simple.
- Easy to compare with the period formula.
- Good for small angles.

Cons:

- It does not show how numerical simulation works step by step.
- It is limited to the ideal small-angle model.

## Option B - Step-by-step numerical update

The current beginner numerical method updates angular velocity and angle at each time step.

Pros:

- Feels more like a simulation.
- Can be extended later to damping.

Cons:

- Needs more care with time step and accuracy.

## Previous proposed first decision

Start with Option A for the first graph, then add a step-by-step method later if the group wants a stronger simulation component.

## What actually happened

The project skipped directly to the step-by-step method. This is still beginner-readable and works well for the current small-angle experiment.

The project also now has an elliptic model helper for comparing the small-angle model against a more realistic non-small-angle solution. That should be treated as extra functionality, not the core first method.

## Open questions

- Should the final report explain semi-implicit Euler in detail, or only describe it briefly?
- Should the elliptic model be included as a stretch goal result?
- Should the group keep using `dt = 0.005 s` for length comparison results?
