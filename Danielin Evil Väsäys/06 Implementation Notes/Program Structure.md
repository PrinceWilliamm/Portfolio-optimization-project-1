---
title: "Program Structure"
tags:
  - python
  - simulation
created: 2026-07-07
status: Active
---

# Program Structure

## Current status

Last checked: 2026-07-07.

The Python project exists outside the Obsidian vault:

```text
K:\Development\Pendulum Simulation Project
```

This resolves the earlier status conflict: the code was not inside the Obsidian project folder, but it does exist in the attached external Python project directory.

## Confirmed structure

```text
K:\Development\Pendulum Simulation Project
|-- pyproject.toml
|-- uv.lock
|-- README.md
|-- src/
|   `-- pendulum_simulation/
|       |-- __init__.py
|       |-- main.py
|       |-- plotting.py
|       `-- simulation.py
|-- experiments/
|   `-- length_comparison.py
|-- outputs/
|   |-- data/
|   |   `-- length_comparison.csv
|   `-- graphs/
|       |-- single_pendulum_angle.png
|       `-- length_comparison.png
|-- tests/
|   `-- test_simulation.py
`-- manim_animations/
    `-- scenes/
        `-- pendulum_intro.py
```

## Confirmed functionality

- Small-angle ideal pendulum simulation using the semi-implicit Euler method.
- Theoretical period calculation using `T = 2*pi*sqrt(L/g)`.
- Simulated period estimation from repeated downward zero crossings.
- Single pendulum angle-over-time graph.
- Length comparison experiment for 0.25 m, 0.5 m, 1.0 m, 1.5 m, and 2.0 m.
- CSV output for length comparison results.
- Elliptic pendulum simulation helper for a more realistic non-small-angle model with zero initial angular velocity.
- Energy calculation helper.
- Simulation variance calculation helper.
- Manim animation comparing the small-angle model and elliptic model.

## Verification

- Tests run on 2026-07-07: 10 passed.
- Warning: pytest reported a cache warning related to `.pytest_cache`, but the tests still passed.
- Git branch: `main`.
- Latest checked commit: `da794fb` - "Animations, elliptic simulation model and variance calculation added".
- Uncommitted change: `manim_animations/scenes/pendulum_intro.py` has animation duration changed from 8.0 s to 20.0 s.

## What is weak

- README mentions `requirements.txt`, but no root `requirements.txt` was found. Dependencies are currently defined in `pyproject.toml` and `uv.lock`.
- The Obsidian notes need to catch up with the code, especially the elliptic model, energy helper, variance helper, and Manim animation.
- Stretch functionality exists before the minimum viable report is finished.

## Next smallest useful task

Use the existing generated results to write the explanation in [[Pendulum Simulation Project/07 Experiments/Length Comparison|Length Comparison]] and then summarize it in [[Pendulum Simulation Project/07 Experiments/Results Summary|Results Summary]].
