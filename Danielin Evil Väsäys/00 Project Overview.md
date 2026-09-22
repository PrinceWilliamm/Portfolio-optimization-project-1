---
title: "00 Project Overview"
project: "Pendulum Simulation Project"
status: "Active"
created: 2026-07-07
source: "[[Pendulum Simulation Project/pendulum_group_project_brief|Project brief]]"
---

# 00 Project Overview

## Current status

Last checked: 2026-07-07.

The project has moved from planning into active implementation and first results. The Obsidian vault contains the project brief, roadmap, task board, dashboard, first theory drafts, and implementation notes. The Python implementation exists in the external code folder `K:\Development\Pendulum Simulation Project`.

Confirmed code status:

- Core simulation package exists in `src/pendulum_simulation/`.
- The first single-pendulum simulation exists and produces an angle-over-time graph.
- The length comparison experiment exists and produces a graph plus CSV results.
- Tests passed on 2026-07-07: 10 passed, with one pytest cache warning.
- The external repository is on git branch `main`, latest checked commit `da794fb`.
- There is one uncommitted external code change: `manim_animations/scenes/pendulum_intro.py` changed animation duration from 8.0 s to 20.0 s.

Confirmed facts from the brief:

- The project is a group research project about a simple pendulum simulation.
- The first version should stay small and focus on the ideal simple pendulum.
- The main workflow is: theory -> model -> simulation -> experiment -> results -> explanation.
- Dee focuses on theory, research, physics, mathematics, and interpretation.
- Bibu focuses on organization, Python implementation, plotting, and development workflow.
- Additional contributors support testing, documentation, feedback, and presentation work.

## Project goal

Create a beginner-friendly research project that explains simple pendulum physics, builds a simple Python simulation, compares results with the theoretical period formula, and presents the findings clearly.

## Minimum viable project

The minimum project should include:

- A clear research question.
- Theory notes explaining the simple pendulum.
- Ideal model assumptions.
- The period formula: `T = 2*pi*sqrt(L/g)`.
- A working Python simulation.
- At least one angle-over-time graph.
- A length comparison experiment.
- A comparison between simulated and theoretical period.
- A short written interpretation.
- A final report or presentation.

## What is done

- [x] Project brief exists: [[Pendulum Simulation Project/pendulum_group_project_brief|Project brief]]
- [x] Contributor notes exist in [[Pendulum Simulation Project/Contributors/Contributor Dee|Contributor Dee]], [[Pendulum Simulation Project/Contributors/Contributor Bibu|Contributor Bibu]], and [[Pendulum Simulation Project/Contributors/Additional Contributors|Additional Contributors]].
- [x] Initial Obsidian structure has been generated.
- [x] Minimum viable research question is drafted in [[Pendulum Simulation Project/01 Research Question|01 Research Question]].
- [x] First implementation output is defined in [[Pendulum Simulation Project/06 Implementation Notes/Simulation Plan|Simulation Plan]].
- [x] First implementation notes exist for functions, numerical method, plotting, and formulas.
- [x] External Python project exists: `K:\Development\Pendulum Simulation Project`.
- [x] Basic semi-implicit Euler simulation is implemented.
- [x] Theoretical period calculation is implemented.
- [x] Simulated period estimation from zero crossings is implemented.
- [x] First angle-over-time graph exists.
- [x] Length comparison experiment exists with graph and CSV data.
- [x] Automated tests exist and pass.
- [x] [[Pendulum Simulation Project/05 Theory/Key Variables|Key Variables]] note exists.
- [x] [[Pendulum Simulation Project/05 Theory/Period Formula|Period Formula]] note exists.

## What is weak

- [ ] The research question still needs group confirmation.
- [ ] Theory notes are drafts and need fuller explanations.
- [ ] Code results need to be explained in student-friendly language.
- [ ] The final report and presentation are not started.
- [ ] [[Pendulum Simulation Project/05 Theory/Key Variables|Key Variables]] and [[Pendulum Simulation Project/05 Theory/Period Formula|Period Formula]] are drafts and need review.
- [ ] The README mentions `requirements.txt`, but no root `requirements.txt` was found.
- [ ] Some stretch functionality exists in code before the research write-up is ready: elliptic model, energy calculation, variance calculation, and Manim animation.

## What should not be built yet

Do not expand these further until the minimum viable write-up is complete:

- Damping simulation.
- Large-angle comparison beyond the existing elliptic model.
- Energy analysis beyond the existing helper function.
- Interactive visualizer.
- Machine learning.
- 3D simulation.
- Real-time physics engine.
- Complex UI.

## Next smallest useful task

Move the clearest length comparison explanation from [[Pendulum Simulation Project/07 Experiments/Length Comparison|Length Comparison]] into [[Pendulum Simulation Project/08 Final Report/Draft Report|Draft Report]].

## Key notes

- [[Pendulum Simulation Project/01 Research Question|01 Research Question]]
- [[Pendulum Simulation Project/02 Roadmap|02 Roadmap]]
- [[Pendulum Simulation Project/03 Task Board|03 Task Board]]
- [[Pendulum Simulation Project/07 Experiments/Length Comparison|Length Comparison]]
- [[Pendulum Simulation Project/08 Final Report/Draft Report|Draft Report]]
