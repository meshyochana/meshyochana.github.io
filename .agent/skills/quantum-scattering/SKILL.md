# Quantum Scattering Simulation Skill

## Goal
To provide precise mathematical analysis and interactive visualizations for 1D quantum mechanical scattering phenomena. This skill helps users understand how particles interact with potential steps, barriers, and wells through the calculation of Transmission (T) and Reflection (R) coefficients.

## Mathematical Core
The skill is based on the following physical models:

### 1. Finite Step Potential
- **Potential**: $V(x) = V_0 \Theta(x)$
- **Reflection ($R_s$ )**:
  - If $\epsilon < 1$: $R_s = 1$ (Total reflection)
  - If $\epsilon > 1$: $R_s = \left(\frac{1 - \sqrt{1 - 1/\epsilon}}{1 + \sqrt{1 - 1/\epsilon}}
ight)^2$
- **Transmission ($T_s$ )**: $T_s = 1 - R_s$

### 2. Finite Potential Barrier
- **Potential**: $V(x) = V_0$ for $-1 < x < 1$, else $0$.
- **Transmission ($T_b$ )**: $T_b = \left(1 + \frac{\sin^2(2q)}{4\epsilon(\epsilon-1)}
ight)^{-1}$
- **Wave Vector ($q$)**: $\sqrt{V_0(\epsilon - 1)}$
- **Note**: For $\epsilon < 1$, use $\sin(ix) = i \sinh(x)$ for tunneling calculations.

### 3. Finite Potential Well
- **Potential**: $V(x) = -V_0$ for $-1 < x < 1$, else $0$.
- **Transmission ($T_w$ )**: $T_w = \left(1 + \frac{\sin^2(2q)}{4\epsilon(\epsilon+1)}\right)^{-1}$
- **Wave Vector ($q$)**: $\sqrt{V_0(\epsilon + 1)}$

## Instructions
1. **Normalization**: Always work with normalized energy $\epsilon = E/V_0$.
2. **Dynamic Sampling**: When generating plots, adjust the step size for $\epsilon$ as $V_0$ increases to avoid aliasing in rapid oscillations (suggested: $	ext{step} \propto 1/\sqrt{V_0}$).
3. **Phenomena Identification**:
   - For Barriers: Identify **Quantum Tunneling** ($\epsilon < 1$) and **Resonances** ($\epsilon > 1$).
   - For Wells: Identify **Transmission Resonances** (Ramsauer-Townsend effect).
4. **Visuals**: Utilize Plotly.js for interactive sliders to allow real-time parameter tuning.

## Constraints
- **Energy Range**: Focus simulations on the range $0 < \epsilon < 5$ for clarity.
- **Accuracy**: Do not approximate the transcendental functions; use exact wave-mechanics solutions.

## Verification
- Ensure $R + T = 1$ is always satisfied (Conservation of Probability).
- Verify that transmission resonances ($T=1$) occur at predictable intervals.