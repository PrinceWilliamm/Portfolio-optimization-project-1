---
title: "Simulation Plan"
project: "Pendulum Simulation Project"
status: "Implemented"
created: 2026-07-07
---

# Simulation Plan

## Current status

Last checked: 2026-07-07.

The first implementation exists in the external Python project:

```text
K:\Development\Pendulum Simulation Project
```

The original smallest useful implementation has been completed: the code can generate pendulum angle values over time, save an angle-over-time graph, estimate the simulated period, and compare it with the theoretical period.

## What is done

- The first output is defined: angle over time.
- Required inputs are listed.
- Required outputs are listed.
- Beginner-readable function names are drafted in [[Pendulum Simulation Project/06 Implementation Notes/Python Function Notes|Python Function Notes]].
- Possible numerical approaches are compared in [[Pendulum Simulation Project/06 Implementation Notes/Numerical Method Notes|Numerical Method Notes]].
- Plot requirements are drafted in [[Pendulum Simulation Project/06 Implementation Notes/Plotting Notes|Plotting Notes]].
- Implemented or intended formulas are collected in [[Pendulum Simulation Project/06 Implementation Notes/Implemented Formulas|Implemented Formulas]].
- Main simulation code exists in `src/pendulum_simulation/simulation.py`.
- First script exists in `src/pendulum_simulation/main.py`.
- Length comparison experiment exists in `experiments/length_comparison.py`.
- Output graph exists: `outputs/graphs/single_pendulum_angle.png`.
- Length comparison graph exists: `outputs/graphs/length_comparison.png`.
- Length comparison data exists: `outputs/data/length_comparison.csv`.
- Tests passed on 2026-07-07: 10 passed, with one pytest cache warning.

## What is weak

- The implementation has grown beyond the original minimum: it now includes an elliptic model, energy calculation, variance calculation, and Manim animation support.
- The code results need better explanation in the Obsidian theory and report notes.
- The root README mentions `requirements.txt`, but the dependency files found were `pyproject.toml` and `uv.lock`.
- The external git working tree has one uncommitted Manim animation change.

## What should not be built yet

- Damping.
- Further large-angle experiments beyond the existing elliptic helper.
- Further energy analysis beyond the existing helper function.
- Interactive UI.
- More Manim animation work until the basic report is written.

## Next smallest useful task

Use the existing outputs to write the interpretation:

1. Explain that the semi-implicit Euler simulation closely matches the theoretical period for small angles.
2. Explain that longer pendulums have longer periods.
3. Move the strongest explanation from [[Pendulum Simulation Project/07 Experiments/Length Comparison|Length Comparison]] into the report draft.
4. Decide whether the current graph should be copied into the Obsidian vault for easier embedding.

## First simulation goal

Generate pendulum angle values over time and plot angle versus time for an ideal simple pendulum.

## Inputs

- Pendulum length `L`.
- Gravity `g`.
- Initial angle `theta_0`.
- Time step `dt`.
- Simulation duration.

## Current first simulation parameters

From `src/pendulum_simulation/main.py`:

| Parameter | Value |
|---|---:|
| Length `L` | 1.0 m |
| Gravity `g` | 9.81 m/s^2 |
| Initial angle | 5 degrees |
| Time step `dt` | 0.01 s |
| Duration | 10.0 s |

## Outputs

- Time values.
- Angle values.
- Angle-over-time graph.
- Estimated simulated period.
- Theoretical period from `T = 2*pi*sqrt(L/g)`.

## Smallest useful implementation

1. Choose fixed values for length, gravity, initial angle, time step, and duration.
2. Generate a list or array of time values.
3. Generate angle values using a beginner-readable model.
4. Plot angle versus time.
5. Save or display the graph.
6. Compare the observed period with the theoretical period.

## Not included in the first report yet

- Damping.
- Full large-angle experiment.
- Full energy analysis.
- Interactive UI.
- Real-world sensor data.
- Manim animation explanation.

## Related notes

- [[Pendulum Simulation Project/06 Implementation Notes/Python Function Notes|Python Function Notes]]
- [[Pendulum Simulation Project/06 Implementation Notes/Numerical Method Notes|Numerical Method Notes]]
- [[Pendulum Simulation Project/06 Implementation Notes/Plotting Notes|Plotting Notes]]
- [[Pendulum Simulation Project/07 Experiments/Length Comparison|Length Comparison]]
