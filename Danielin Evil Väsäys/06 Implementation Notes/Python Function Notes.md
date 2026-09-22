---
title: "Python Function Notes"
project: "Pendulum Simulation Project"
status: "Implemented"
created: 2026-07-07
---

# Python Function Notes

## Goal

Keep the Python code beginner-readable and small.

## Current status

Last checked: 2026-07-07.

The main beginner-readable functions now exist in the external Python project:

```text
K:\Development\Pendulum Simulation Project\src\pendulum_simulation
```

## Implemented functions

```python
def theoretical_period(length_m, gravity_m_s2):
    """Return the ideal small-angle pendulum period."""


def simulate_pendulum(parameters):
    """Simulate an ideal simple pendulum using the semi-implicit Euler method."""


def estimate_period(result):
    """Estimate period from repeated downward zero crossings."""


def plot_angle_over_time(result, output_path):
    """Save one angle-over-time graph."""
```

Additional implemented helpers:

- `validate_parameters(parameters)`
- `simulate_pendulum_elliptic(parameters)`
- `calculate_energy(result)`
- `calculate_simulation_variance(first_result, second_result)`
- `plot_length_comparison(results, output_path)`

## Design rules

- Use clear variable names.
- Prefer simple functions over clever code.
- Avoid premature architecture.
- Add comments only where they explain the physics or algorithm.
- Do not add UI until the core simulation works.

## Open questions

- Should plots stay in radians, or should the report convert the y-axis to degrees for readability?
- Should the elliptic model be included in the final report, or saved as a future improvement?
- Should the energy and variance helpers be documented now, or postponed until after the minimum report?
