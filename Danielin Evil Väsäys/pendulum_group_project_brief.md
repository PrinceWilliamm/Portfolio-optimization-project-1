---
title: "Project N.1 — Pendulum Simulation Research"
project_type: "Group research project"
status: "Planning"
tags:
  - physics
  - mathematics
  - simulation
  - python
  - research
  - collaboration
  - pendulum
created: 2026-07-07
---

# Project N.1 — Pendulum Simulation Research

## 1. Project idea

The group will build a small research project around the **simple pendulum**.

The project will compare the ideal mathematical model of pendulum motion with a simple computational simulation. The main goal is to understand how pendulum behavior depends on length, gravity, starting angle, and damping.

This project is intentionally small. It is meant to help the group practice working together on a complete research workflow:

> Theory → Model → Simulation → Experiment → Results → Explanation

The project should not begin as an advanced software project. The first version should focus on understanding the physics, writing clear research notes, creating a simple simulation, and interpreting the results.

---

## 2. Main research question

> How does a simple pendulum behave under the ideal model, and how do variables like length, gravity, initial angle, and damping affect its motion?

---

## 3. Core concept

A pendulum is a mass hanging from a fixed point by a string or rod. When displaced from its resting position and released, gravity pulls it back toward equilibrium, causing oscillatory motion.

In the ideal model, the assumptions are:

- The string or rod is massless.
- The pendulum bob is treated as a point mass.
- There is no air resistance.
- There is no friction at the pivot.
- Gravity is constant.
- The motion happens in a single vertical plane.
- The angle is small enough for the small-angle approximation to be useful.

For small angles, the pendulum behaves approximately like simple harmonic motion.

The approximate equation for the period of a simple pendulum is:

```math
T = 2\pi\sqrt{\frac{L}{g}}
```

Where:

| Symbol | Meaning |
|---|---|
| `T` | Period of one full swing |
| `L` | Length of the pendulum |
| `g` | Gravitational acceleration |
| `π` | Pi, approximately 3.14159 |

This formula predicts that the period depends on the pendulum length and gravity, but not on the mass of the pendulum bob.

---

## 4. Project goal

The goal is to create a complete beginner-friendly research project that includes:

1. A clear explanation of pendulum physics.
2. A mathematical model of the simple pendulum.
3. A simple Python simulation.
4. Graphs showing pendulum angle, velocity, or position over time.
5. Experiments with different pendulum lengths, gravity values, and starting angles.
6. A written interpretation of the results.
7. A final report or presentation.

The project should help the group practice:

- Physics reasoning
- Mathematical modeling
- Python programming
- Numerical simulation
- Data visualization
- Scientific writing
- Collaborative project execution

---

## 5. Minimum viable project

The first finished version should include only the essential components.

## Version 1 requirements

- Explain what a simple pendulum is.
- Explain the ideal assumptions.
- Explain the period formula:

```math
T = 2\pi\sqrt{\frac{L}{g}}
```

- Implement a simple Python simulation.
- Allow changing:
  - Pendulum length
  - Initial angle
  - Gravity
  - Time step
  - Simulation duration
- Generate pendulum angle values over time.
- Plot the pendulum angle over time.
- Compare different pendulum lengths.
- Compare the simulated period with the theoretical period.
- Write a short conclusion.

## Version 1 research experiment

Test pendulum lengths such as:

- 0.25 m
- 0.5 m
- 1.0 m
- 1.5 m
- 2.0 m

Compare:

- Period of oscillation
- Shape of angle-over-time graph
- How changing length affects swing speed
- Difference between theoretical and simulated period

Expected ideal-model result:

> A longer pendulum should have a longer period, meaning it swings more slowly.

---

## 6. Possible stretch goals

These should only be added after the minimum viable project is complete.

## Stretch goal A — Damping

Add a simple damping term to model energy loss from air resistance or friction.

Research question:

> How does damping change the amplitude of pendulum motion over time?

Expected behavior:

> The pendulum should gradually lose energy, causing the swing amplitude to decrease.

---

## Stretch goal B — Large-angle pendulum

Investigate what happens when the initial angle is no longer small.

Research question:

> When does the small-angle approximation stop being accurate?

This can compare:

- 5°
- 10°
- 20°
- 45°
- 70°

Expected behavior:

> The small-angle approximation works well for small angles but becomes less accurate as the initial angle increases.

---

## Stretch goal C — Gravity comparison

Compare pendulum behavior under different gravitational fields.

| Location | Approximate gravity |
|---|---:|
| Moon | 1.62 m/s² |
| Mars | 3.71 m/s² |
| Earth | 9.81 m/s² |
| Jupiter | 24.79 m/s² |

Research question:

> How does gravity affect the period of a pendulum?

Expected behavior:

> Stronger gravity should produce a shorter period, meaning the pendulum swings faster.

---

## Stretch goal D — Energy analysis

Track kinetic energy, potential energy, and total mechanical energy.

Research question:

> How does energy change in an ideal pendulum compared with a damped pendulum?

Expected ideal-model behavior:

> In the ideal model, total mechanical energy should remain approximately constant.

Expected damped-model behavior:

> In the damped model, total mechanical energy should decrease over time.

---

## Stretch goal E — Interactive visualizer

Build a simple interface with sliders for:

- Length
- Gravity
- Initial angle
- Damping
- Simulation duration

Possible tools:

- Streamlit
- Jupyter Notebook widgets
- Simple command-line interface

This should not be added until the basic simulation and research report are complete.

---

# 7. Work distribution

The project should be divided so each contributor has a meaningful role based on current skills and desired learning areas.

---

## Contributor Dee

## Main role

**Theory, research, physics explanation, mathematical reasoning, and interpretation.**

## Responsibilities

- Research simple pendulum theory.
- Explain the physical system.
- Explain the ideal assumptions.
- Explain the small-angle approximation.
- Explain the period formula.
- Research how damping affects pendulum motion if stretch goals are reached.
- Research when the small-angle approximation fails.
- Write theory notes in Obsidian.
- Interpret graphs and results.
- Help write the final report.

## Learning focus

- Classical mechanics
- Oscillatory motion
- Mathematical modeling
- Small-angle approximation
- Research methods
- Scientific writing
- Connecting equations to simulated behavior

## Suggested first tasks

- Create a note called `Simple Pendulum Theory.md`.
- Write a beginner-friendly explanation of pendulum motion.
- Define period, amplitude, length, gravity, angular displacement, and equilibrium.
- Explain the assumptions of the ideal pendulum model.
- Research why pendulum period depends on length and gravity.
- Research why mass does not affect the period in the ideal model.
- Write a short explanation of the small-angle approximation.

---

## Contributor Bibu

## Main role

**Project organization, implementation, simulation, tooling, visualization, and development workflow.**

## Responsibilities

- Set up the project folder structure.
- Set up the Obsidian project workspace.
- Use Claudian to manage planning and execution.
- Create the Python simulation.
- Generate pendulum motion data.
- Create graphs.
- Organize code and documentation.
- Maintain the project roadmap.
- Maintain the task board.
- Convert research notes into implementation tasks.
- Keep the project scope realistic.

## Learning focus

- Python
- Numerical simulation
- Plotting and visualization
- Project structure
- Documentation workflow
- Research-to-code implementation
- Scientific computing basics

## Suggested first tasks

- Create the project directory.
- Create a basic Python file for the simulation.
- Write a function that estimates pendulum motion over time.
- Plot angle versus time.
- Add parameter variables for length, gravity, initial angle, time step, and duration.
- Create a results note in Obsidian.
- Ask Claudian to generate the project roadmap and task breakdown from this file.

---

## Additional contributors

## Main role

**Support, testing, documentation, presentation, and feedback.**

## Responsibilities

- Help review explanations.
- Test different simulation inputs.
- Help collect results.
- Help compare graphs.
- Help check whether explanations are understandable.
- Help write summaries.
- Help prepare final presentation materials.
- Ask beginner-level questions to expose unclear explanations.

## Learning focus

- Collaborative research
- Basic physics intuition
- Reading graphs
- Scientific communication
- Project participation
- Testing and observation

## Suggested first tasks

- Test the simulation using different pendulum lengths.
- Record observations.
- Help compare graphs.
- Write simple explanations of what the results show.
- Help improve the final report.
- Help prepare a presentation outline.

---

# 8. Suggested Obsidian structure

The project planning, research, and execution notes should live in Obsidian.

Suggested structure:

```text
Pendulum Simulation Research/
├── 00 Project Overview.md
├── 01 Research Question.md
├── 02 Roadmap.md
├── 03 Task Board.md
├── 04 Meeting Notes/
│   └── Meeting 01.md
├── 05 Theory/
│   ├── Simple Pendulum Theory.md
│   ├── Assumptions of the Ideal Model.md
│   ├── Key Variables.md
│   ├── Period Formula.md
│   ├── Small-Angle Approximation.md
│   └── Limitations of the Ideal Model.md
├── 06 Implementation Notes/
│   ├── Simulation Plan.md
│   ├── Python Function Notes.md
│   ├── Numerical Method Notes.md
│   └── Plotting Notes.md
├── 07 Experiments/
│   ├── Length Comparison.md
│   ├── Gravity Comparison.md
│   ├── Initial Angle Comparison.md
│   ├── Damping Experiment.md
│   └── Results Summary.md
├── 08 Final Report/
│   ├── Draft Report.md
│   └── Final Report.md
└── 09 Presentation/
    └── Presentation Outline.md
```

---

# 9. Suggested code project structure

The code structure can be created later after the research plan is stable.

Suggested structure:

```text
pendulum-simulation/
├── README.md
├── requirements.txt
├── src/
│   ├── main.py
│   ├── simulation.py
│   └── plotting.py
├── experiments/
│   ├── length_comparison.py
│   ├── gravity_comparison.py
│   └── angle_comparison.py
├── outputs/
│   ├── graphs/
│   └── data/
└── notes/
    └── development_notes.md
```

This structure should be generated later by the AI agent or created manually after the roadmap is defined.

---

# 10. Recommended development phases

---

## Phase 1 — Planning

Goal:

> Define the project clearly before writing code.

Tasks:

- Agree on the research question.
- Define the minimum viable project.
- Assign roles.
- Create the Obsidian project structure.
- Create a task board.
- Decide what the first result should look like.

Deliverable:

- Project overview note
- Research question note
- Initial task list

---

## Phase 2 — Theory

Goal:

> Understand the physics model before implementing it.

Tasks:

- Research simple pendulum motion.
- Define all variables.
- Write down ideal assumptions.
- Explain the period formula.
- Explain small-angle approximation.
- Explain model limitations.

Deliverable:

- Theory notes
- Equation notes
- Assumption notes

---

## Phase 3 — Basic simulation

Goal:

> Create a working Python simulation of ideal pendulum motion.

Tasks:

- Create basic Python files.
- Implement pendulum motion approximation.
- Generate time values.
- Calculate angle values over time.
- Plot angle against time.
- Save the first graph.

Deliverable:

- A graph of pendulum angle over time

---

## Phase 4 — Experiments

Goal:

> Use the simulation to answer simple research questions.

Tasks:

- Test multiple pendulum lengths.
- Test different initial angles.
- Compare simulated period with theoretical period.
- Save graphs.
- Write observations in Obsidian.

Deliverable:

- Length comparison graph
- Results table
- Written interpretation

---

## Phase 5 — Report

Goal:

> Turn the work into a clear research output.

Tasks:

- Summarize the theory.
- Explain the simulation.
- Present graphs.
- Interpret results.
- Explain limitations.
- List possible future improvements.

Deliverable:

- Final written report or presentation

---

# 11. Research documentation expectations

Every research note should try to answer these questions:

1. What is the concept?
2. Why does it matter for the project?
3. What equations or definitions are needed?
4. What assumptions are being made?
5. What are the limitations?
6. How does this connect to the simulation?

A good research note should be understandable by someone who knows basic high-school physics and mathematics.

---

# 12. Code expectations

The code should be simple and readable.

Priority order:

1. Correctness
2. Clarity
3. Reusability
4. Visualization
5. Optimization

Do not optimize performance early. The simulation is small.

Recommended Python libraries:

- `math`
- `numpy`
- `matplotlib`

Optional later:

- `pandas`
- `streamlit`

---

# 13. Important scope control

Avoid adding too much too early.

Do not start with:

- Machine learning
- Advanced differential equation solvers
- Complex graphical UI
- 3D simulation
- Game engine implementation
- Real-time physics engine
- Large database systems
- Real-world sensor measurements
- Complex experimental hardware

These can be future projects, not the first version.

The first goal is:

> One clear research question, one working simulation, one graph, one explanation.

---

# 14. Suggested first Claudian prompt

Use this prompt in Obsidian with the Claudian plugin after importing this file:

```text
You are helping manage a small group research project in Obsidian.

Read the project brief in this note.

Generate:
1. A clean Obsidian folder and note structure.
2. A beginner-friendly project roadmap.
3. A task board divided by contributor role.
4. A first-week execution plan.
5. A definition of done for the minimum viable project.

Constraints:
- Keep the project small and realistic.
- The first project is about pendulum simulation.
- Dee focuses on theory, research, physics, mathematics, and interpretation.
- Bibu focuses on implementation, project organization, Python, plotting, and development workflow.
- Additional contributors help with testing, writing, presentation, and feedback.
- Avoid advanced features until the minimum viable version is complete.
```

---

# 15. Suggested first research prompt

Use this prompt to generate the first theory notes:

```text
Create beginner-friendly research notes for a simple pendulum simulation project.

Explain:
1. What a simple pendulum is.
2. What period, amplitude, length, gravity, and equilibrium mean.
3. The assumptions of the ideal pendulum model.
4. The period formula T = 2π√(L/g).
5. Why mass does not affect the period in the ideal model.
6. What the small-angle approximation means.
7. What limitations the ideal model has.

Write the explanation for students who know basic high-school physics and mathematics.
```

---

# 16. Suggested first coding prompt

Use this later, after the theory and roadmap are ready:

```text
Create a beginner-friendly Python implementation plan for an ideal simple pendulum simulation.

The implementation should:
- Use simple functions.
- Allow changing pendulum length, initial angle, gravity, timestep, and simulation duration.
- Generate angle values over time.
- Plot angle versus time with matplotlib.
- Compare simulated period with the theoretical formula T = 2π√(L/g).
- Be organized into readable files.

Do not add damping yet.
Do not create a UI yet.
```

---

# 17. Definition of done

The minimum project is complete when the group has:

- A clear research question.
- Theory notes explaining simple pendulum motion.
- Notes explaining the ideal assumptions.
- Notes explaining the period formula.
- A working Python simulation.
- At least one angle-over-time graph.
- A length comparison experiment.
- A comparison between simulated and theoretical period.
- A short written interpretation of the results.
- A final report or presentation.
- A list of future improvements.

---

# 18. Final project summary

This project is a small scientific modeling project based on pendulum motion.

It connects:

- Dee's physics and mathematics interests
- Bibu's programming and project development focus
- Additional contributors' support in testing, documentation, and presentation

The project is intentionally simple at the beginning. Its value comes from completing the full research cycle:

> Theory → Model → Simulation → Experiment → Results → Explanation

The first version should stay focused on the ideal simple pendulum. More advanced features, such as damping, large-angle behavior, energy analysis, and interactive controls, should only be added after the basic version is complete.
