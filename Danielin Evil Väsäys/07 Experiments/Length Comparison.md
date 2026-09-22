---
title: "Length Comparison"
project: "Pendulum Simulation Project"
status: "Results recorded"
created: 2026-07-07
---

# Length Comparison

## Research question

How does changing pendulum length affect the period and angle-over-time graph?

## Expected ideal-model result

A longer pendulum should have a longer period, meaning it swings more slowly.

## Current status

Last checked: 2026-07-07.

The length comparison experiment has been implemented in the external Python project:

```text
K:\Development\Pendulum Simulation Project\experiments\length_comparison.py
```

Confirmed outputs:

- Graph: `K:\Development\Pendulum Simulation Project\outputs\graphs\length_comparison.png`
- Data: `K:\Development\Pendulum Simulation Project\outputs\data\length_comparison.csv`

## Controlled variables

- Gravity: 9.81 m/s^2.
- Initial angle: small and constant.
- Time step: constant.
- Duration: long enough to show multiple swings.

## Lengths to test

| Length | Theoretical period | Simulated period | Observation |
|---:|---:|---:|---|
| 0.25 m | 1.003033 s | 1.002992 s | Fastest swing; shortest period. |
| 0.5 m | 1.418503 s | 1.418474 s | Longer than 0.25 m. |
| 1.0 m | 2.006067 s | 2.006046 s | About 2 seconds per period. |
| 1.5 m | 2.456920 s | 2.456903 s | Slower than 1.0 m. |
| 2.0 m | 2.837007 s | 2.836992 s | Slowest swing; longest period. |

## Accuracy

| Length | Percent error |
|---:|---:|
| 0.25 m | 0.0041% |
| 0.5 m | 0.0020% |
| 1.0 m | 0.0010% |
| 1.5 m | 0.0007% |
| 2.0 m | 0.0005% |

## Procedure

1. Run the simulation for each length.
2. Save or display the angle-over-time graph.
3. Estimate the simulated period.
4. Calculate the theoretical period.
5. Compare the values.
6. Write observations.

## Results

The results match the expected ideal-model behavior:

- Longer pendulums have longer periods.
- Shorter pendulums swing faster.
- The simulated period is extremely close to the theoretical period for the tested small-angle setup.

## Interpretation

The result supports the first-version research question. In the ideal small-angle model, pendulum length strongly affects the period. Increasing the length increases the period, so the pendulum completes each swing more slowly.

The simulation agrees closely with the theoretical formula:

```text
T = 2*pi*sqrt(L/g)
```

This is expected because the experiment used a small initial angle of 5 degrees, Earth gravity, and the same ideal assumptions as the theoretical model.

## Remaining work

- Add the graph image to the final report or presentation.
- Explain the result in beginner-friendly language.
- Mention that this result only applies to the ideal small-angle model.
