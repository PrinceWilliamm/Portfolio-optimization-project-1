
# Pendulum Simulation Project Dashboard

## Main links

- [[Pendulum Simulation Project/pendulum_group_project_brief|Project brief]]
- [[Pendulum Simulation Project/00 Project Overview|00 Project Overview]]
- [[Pendulum Simulation Project/01 Research Question|01 Research Question]]
- [[Pendulum Simulation Project/02 Roadmap|02 Roadmap]]
- [[Pendulum Simulation Project/03 Task Board|03 Task Board]]
- [[Pendulum Simulation Project/04 Meeting Notes/Meeting 01|Meeting 01]]

## Work areas

- [[Pendulum Simulation Project/05 Theory/Simple Pendulum Theory|Theory notes]]
- [[Pendulum Simulation Project/06 Implementation Notes/Simulation Plan|Implementation notes]]
- [[Pendulum Simulation Project/07 Experiments/Length Comparison|Experiments]]
- [[Pendulum Simulation Project/08 Final Report/Draft Report|Final report]]
- [[Pendulum Simulation Project/09 Presentation/Presentation Outline|Presentation]]

## Contributors

- [[Pendulum Simulation Project/Contributors/Contributor Dee|Contributor Dee]] - theory, physics, mathematics, interpretation
- [[Pendulum Simulation Project/Contributors/Contributor Bibu|Contributor Bibu]] - organization, implementation, plotting, workflow
- [[Pendulum Simulation Project/Contributors/Additional Contributors|Additional Contributors]] - testing, documentation, feedback, presentation support

## Current status

- Last checked: 2026-07-07.
- Project status: active implementation / first results recorded.
- Minimum viable goal: one clear research question, one working simulation, one graph, one explanation.
- Confirmed in the vault:
  - Project brief, roadmap, task board, dashboard, and contributor notes exist.
  - The minimum viable research question is drafted in [[Pendulum Simulation Project/01 Research Question|01 Research Question]].
  - First theory drafts exist for [[Pendulum Simulation Project/05 Theory/Simple Pendulum Theory|Simple Pendulum Theory]], [[Pendulum Simulation Project/05 Theory/Assumptions of the Ideal Model|Assumptions of the Ideal Model]], [[Pendulum Simulation Project/05 Theory/Key Variables|Key Variables]], [[Pendulum Simulation Project/05 Theory/Period Formula|Period Formula]], and [[Pendulum Simulation Project/05 Theory/Small-Angle Approximation|Small-Angle Approximation]].
  - Implementation planning exists in [[Pendulum Simulation Project/06 Implementation Notes/Simulation Plan|Simulation Plan]], [[Pendulum Simulation Project/06 Implementation Notes/Python Function Notes|Python Function Notes]], [[Pendulum Simulation Project/06 Implementation Notes/Numerical Method Notes|Numerical Method Notes]], [[Pendulum Simulation Project/06 Implementation Notes/Plotting Notes|Plotting Notes]], and [[Pendulum Simulation Project/06 Implementation Notes/Implemented Formulas|Implemented Formulas]].
  - [[Pendulum Simulation Project/07 Experiments/Length Comparison|Length Comparison]] now has recorded results from the external Python project.
- Confirmed in the external Python project:
  - Code folder: `K:\Development\Pendulum Simulation Project`
  - Git branch: `main`, latest commit checked: `da794fb` - "Animations, elliptic simulation model and variance calculation added".
  - Core package exists in `src/pendulum_simulation/`.
  - First simulation script exists: `src/pendulum_simulation/main.py`.
  - Length comparison script exists: `experiments/length_comparison.py`.
  - Generated graphs exist: `outputs/graphs/single_pendulum_angle.png` and `outputs/graphs/length_comparison.png`.
  - Length comparison data exists: `outputs/data/length_comparison.csv`.
  - Tests passed on 2026-07-07: 10 passed, with one pytest cache warning.
- Not finished yet:
  - The final report and presentation are not started.
  - Theory notes still need fuller explanations.
  - Results still need to be interpreted in the final report.
  - The README mentions `requirements.txt`, but the root project currently uses `pyproject.toml` and `uv.lock`; no root `requirements.txt` was found.
  - The external git working tree has one uncommitted change in `manim_animations/scenes/pendulum_intro.py`: animation duration changed from 8.0 s to 20.0 s.

## Next smallest useful task

- Dee: expand the theory notes so they explain the code results clearly.
- Bibu: clean up the documentation/code mismatch about `requirements.txt` and decide whether to commit the Manim duration change.
- Group: use [[Pendulum Simulation Project/07 Experiments/Length Comparison|Length Comparison]] and [[Pendulum Simulation Project/07 Experiments/Results Summary|Results Summary]] as the basis for the report interpretation.
