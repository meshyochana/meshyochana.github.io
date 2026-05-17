---
name: quantum-simulation-expert
description: Guidelines for developing high-fidelity, interactive quantum mechanics simulations with accurate math rendering, dynamic plotting, and proper attribution.
---

# General Quantum Simulation Skill

## 1. Mathematical Rendering
To ensure equations are readable across all platforms (web, notebooks, and IDEs), follow these LaTeX/MathJax standards:

- **Delimiters**: Always use standard LaTeX delimiters. 
  - Inline: `\( ... \)` or `$ ... $`
  - Display/Block: `\\[ ... \\]` or `$$...$$`
- **Contextual Physics**: Always normalize energies (e.g., \(\epsilon = E/V_0\\)) and wave vectors to make results scale-invariant and easier for students to interpret.
- **Complex Logic**: When representing tunneling, explicitly use hyperbolic functions (e.g., \(\sinh\\), \(\cosh\\)) instead of imaginary trigonometric arguments to avoid rendering or computation errors in standard JavaScript environments.

## 2. Interactive Visualization (Plotly)
When creating interactive simulations for students, use Plotly.js for its responsiveness and built-in toolsets.

### Anti-Aliasing & Dynamic Sampling
As potential parameters (like \(V_0\\)) increase, the frequency of oscillations in transmission/reflection coefficients increases. To avoid visual artifacts (aliasing):
- **Variable Mesh**: Calculate the x-axis step size as a function of the potential strength.
- **Suggested Formula**: `let stepSize = Math.max(0.0005, 0.01 / Math.sqrt(V0 + 1));`
- **Efficiency**: This ensures high resolution only when needed, maintaining browser performance.

### UI Layout
- **Explanations**: Always place a "What is calculated" and "How to interpret" section directly above or beside the plot.
- **Sliders**: Provide intuitive controls for physical constants (Potential height, barrier width, incident energy).
- **Hover Modes**: Enable `hovermode: 'x unified'` to allow students to compare Reflection (R) and Transmission (T) values at precise energy levels.

## 3. Standard Credit Line
All simulations derived from this framework should include the following attribution to acknowledge the original pedagogical source:

> **Source/Credit**: Ron Lifshitz, Tel Aviv University, 2011 (Updated 2020).

## 4. Implementation Checklist
- [ ] Is probability conserved? (Verify \(R + T = 1\\))
- [ ] Are transmission resonances clearly visible at \(T=1\\)?
- [ ] Does the math render correctly without raw LaTeX code showing?
- [ ] Is the sampling fine enough to show smooth curves at maximum slider values?