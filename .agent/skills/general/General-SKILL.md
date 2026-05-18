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
- **Universal Typesetting**: Ensure proper LaTeX-style math rendering everywhere. Text boxes should use MathJax, while Plotly graphs must natively parse LaTeX strings (using `$...$`) for all plot titles, axis titles, legends, and trace names so that variables like $\hat{V}_0$ render correctly across the entire interface.

## 2. Interactive Visualization (Plotly)
When creating interactive simulations for students, use Plotly.js for its responsiveness and built-in toolsets.

### Anti-Aliasing & Dynamic Sampling
As potential parameters (like \(V_0\\)) increase, the frequency of oscillations in transmission/reflection coefficients increases. To avoid visual artifacts (aliasing):
- **Variable Mesh**: Calculate the x-axis step size as a function of the potential strength.
- **Suggested Formula**: `let stepSize = Math.max(0.0005, 0.01 / Math.sqrt(V0 + 1));`
- **Efficiency**: This ensures high resolution only when needed, maintaining browser performance.

### Responsive & Aspect-Ratio Scaling
- **Adaptive Layout**: Ensure all content fits on the screen without scrolling. Use CSS viewport units (`vh`) for plot heights and enable Plotly's `{responsive: true}` configuration.
- **Equal Axes Scale**: When plotting intersecting curves (like $k$ vs $\beta$), lock the axes to a 1:1 aspect ratio (`scaleanchor: 'x', scaleratio: 1`).
- **Adjustable vs Fixed Graphs**: By default, graphs should dynamically scale axes to fit the current data, but provide UI toggle buttons (e.g. "Lock Axes") that allow users to fix the $x$ and $y$ ranges for stable comparison as parameters change.

### UI Layout
- **Explanations**: Always place a "What is calculated" and "How to interpret" section directly above or beside the plot.
- **Sliders**: Provide intuitive controls for physical constants (Potential height, barrier width, incident energy).
- **Hover Modes**: Enable `hovermode: 'x unified'` to allow students to compare Reflection (R) and Transmission (T) values at precise energy levels.

## 3. Advanced Simulation Architecture

### Memory Management & Performance (60 FPS Sliders)
When tying physics calculations to a UI slider, the browser has to recalculate and redraw the plot dozens of times per second. 
- **Guideline**: Avoid dynamically creating new arrays inside loops. Pre-allocate Javascript Typed Arrays (like `new Float64Array()`) globally and overwrite their values on each slider update. This prevents the browser's Garbage Collector from freezing the UI due to thousands of abandoned arrays, ensuring buttery-smooth interactivity.

### Numerical Stability Strategies
Quantum mechanics equations often involve singularities (like $\tan(k)$ going to infinity) or exponential decay that can cause floating-point overflow.
- **Guideline**: Prefer robust, bounded algorithms. For example, use Bisection root-finding within strictly defined analytical brackets (like between $0$ and $\pi/2$) rather than relying on unconstrained Newton-Raphson solvers, which will violently diverge near asymptotes. Cap exponential growths in forbidden regions to avoid `Infinity` rendering errors.

### Visual Linking (Color Coding)
Physics UI can be dense. Students learn faster when the math is visually tied to the graphs.
- **Guideline**: Strictly map colors between mathematical text and graphical traces. If the even state curve is plotted in red, the inline MathJax equation explaining it in the text should also be colored red (e.g., `\color{red}{\hat{\beta} = \hat{k}\tan \hat{k}}`).

## 4. Standard Credit Line
All simulations derived from this framework should include the following attribution to acknowledge the original pedagogical source:

> **Source/Credit**: Converted and updated by Meshy Ochana (2026) from Ron Lifshitz's Mathematica Notebook (...the relevant year...)

## 5. Implementation Checklist
- [ ] Is probability conserved? (Verify \(R + T = 1\\))
- [ ] Are transmission resonances clearly visible at \(T=1\\)?
- [ ] Does the math render correctly without raw LaTeX code showing?
- [ ] Is the sampling fine enough to show smooth curves at maximum slider values?