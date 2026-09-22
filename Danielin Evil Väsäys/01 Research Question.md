---
title: "01 Research Question"
project: "Pendulum Simulation Project"
status: "Draft"
created: 2026-07-07
source: "[[Pendulum Simulation Project/pendulum_group_project_brief|Project brief]]"
---

# 01 Research Question

## Main research question

How does a simple pendulum behave under the ideal model, and how do variables like length, gravity, initial angle, and damping affect its motion?

## Minimum viable version question

For the first version, focus on this smaller question:

> How does changing the length of an ideal simple pendulum affect its period and angle-over-time graph?

## Subquestions

- What is a simple pendulum?
- What assumptions are used in the ideal model?
- Why does the period depend on length and gravity?
- Why does mass not affect the ideal pendulum period?
- How close is the simulated period to the theoretical period?
- What changes in the graph when pendulum length changes?

## Variables

| Variable | Role in first version | Notes |
|---|---|---|
| Length `L` | Main independent variable | Test 0.25 m, 0.5 m, 1.0 m, 1.5 m, 2.0 m |
| Gravity `g` | Controlled variable | Use Earth gravity first: 9.81 m/s^2 |
| Initial angle | Controlled variable | Keep small for the first version |
| Time step `dt` | Simulation setting | Needs to be small enough for smooth graphs |
| Duration | Simulation setting | Long enough to show multiple swings |
| Mass | Not included | Ideal model predicts mass does not affect period |

## Scope decision

First version:

- Use the ideal simple pendulum model.
- Use small angles.
- Plot angle versus time.
- Compare theoretical and simulated period.

Later versions may study damping, large angles, gravity comparison, and energy.
