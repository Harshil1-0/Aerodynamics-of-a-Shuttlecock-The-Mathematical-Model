Aerodynamics of a Shuttlecock: The Mathematical Model

A B.Tech Computation & Mathematics project that looks at badminton shuttlecock flight through its mathematics: dimensionless numbers, force balances, the continuity and Navier–Stokes equations, and complex-potential (conformal mapping) arguments for comparing shuttlecock designs.

**Team:** Gnanada Vanaparthi, Harshil, Shoa Ahmed, Shirsha, Venkat
**Guide:** Dr. Satyanarayana Chirala
**Programme:** B.Tech. in Computation & Mathematics (2024 batch), Department of Mathematics, École Centrale School of Engineering, Mahindra University, Hyderabad

> Math is written in LaTeX, which renders on GitHub. Sections marked *(extension)* are standard derivations added to complete the report's formulas; they are not in the original report.

---

## 1. Notation

| Symbol | Meaning | Unit |
|--------|---------|------|
| $\rho$ | air density | kg/m³ |
| $\mu$ | dynamic viscosity of air | Pa·s |
| $V$ | shuttlecock speed | m/s |
| $D$, $L$ | characteristic length (skirt diameter) | m |
| $A$ | cross-sectional area | m² |
| $m$ | shuttlecock mass | kg |
| $g$ | gravitational acceleration | m/s² |
| $\mathbf{u}$ | velocity field | m/s |
| $p$ | pressure | Pa |

## 2. Force and Dimensionless Models

**Drag force**

$$F_D = \tfrac12 C_D\,\rho\,A\,V^2 \qquad\Longleftrightarrow\qquad C_D = \frac{2F_D}{\rho A V^2}$$

The drag coefficient $C_D$ is dimensionless. The report gives $C_D \approx 0.7$–$1.0$ for shuttlecocks.

**Pressure (form) drag.** Drag from the front–rear pressure difference:

$$\Delta P = P_{\text{front}} - P_{\text{rear}}, \qquad F_D = \Delta P \cdot A$$

**Lift force**

$$L = \tfrac12\,\rho\,V^2 A\,C_L$$

The report treats $C_L$ as small compared with $C_D$ (from asymmetry or spin), so lift matters for trajectory stability rather than range.

**Reynolds number** (ratio of inertial to viscous effects; predicts laminar vs turbulent flow)

$$\mathrm{Re} = \frac{\rho V D}{\mu}$$

**Strouhal number** (dimensionless vortex-shedding frequency in the wake)

$$\mathrm{St} = \frac{fL}{V} \quad\Longrightarrow\quad f = \frac{\mathrm{St}\,V}{L}$$

**Terminal velocity.** Set drag equal to weight, $\tfrac12 C_D \rho A V_t^2 = mg$:

$$V_t = \sqrt{\frac{2mg}{C_D\,\rho\,A}}$$

Since $V_t \propto \sqrt{1/(C_D A)}$, a larger $C_D A$ (bigger skirt, more drag) gives a lower terminal speed. The report quotes $V_t \approx 6$–$7$ m/s.

## 3. Worked Numerical Example *(extension)*

Illustrative values: $m = 5\ \text{g}$, $D = 0.062\ \text{m}$, $C_D = 0.7$, $\rho = 1.2\ \text{kg/m}^3$, $\mu = 1.81\times10^{-5}\ \text{Pa·s}$.

$$A = \pi\left(\tfrac{D}{2}\right)^2 \approx 3.02\times10^{-3}\ \text{m}^2$$

$$V_t = \sqrt{\frac{2(0.005)(9.81)}{0.7\,(1.2)\,(3.02\times10^{-3})}} \approx 6.2\ \text{m/s}$$

This is consistent with the report's 6–7 m/s. Reynolds numbers:

$$\mathrm{Re}\big|_{V=6.2} \approx \frac{1.2(6.2)(0.062)}{1.81\times10^{-5}} \approx 2.5\times10^{4}, \qquad \mathrm{Re}\big|_{V=100} \approx 4.1\times10^{5}$$

So the shuttlecock spans roughly $10^4$ to $10^5$–$10^6$ in Re over a rally, from a fast smash down to the slow descent.

## 4. Equation of Motion for a Falling Shuttlecock *(extension)*

For vertical fall, Newton's second law gives the nonlinear ODE

$$m\frac{dv}{dt} = mg - \tfrac12 C_D\rho A\,v^2 \quad\Longleftrightarrow\quad \frac{dv}{dt} = g\left(1 - \frac{v^2}{V_t^2}\right).$$

It is separable. With $v(0)=0$,

$$v(t) = V_t \tanh\!\left(\frac{g\,t}{V_t}\right).$$

Properties:

- $v(t)\to V_t$ as $t\to\infty$ (the terminal velocity is the stable equilibrium of the ODE)
- The time scale is $\tau = V_t/g \approx 0.63$ s for the example above
- At $t = 1$ s, $v \approx V_t\tanh(1.58) \approx 0.92\,V_t$, which matches the report's remark that a shuttle reaches terminal velocity within about a second

## 5. Governing Equations

**Mass conservation (continuity).** For incompressible flow (subsonic air around a shuttlecock),

$$\nabla\cdot\mathbf{u} = 0,$$

i.e. the velocity field is divergence-free: net outflow per unit volume is zero. Bleed-through of air in the skirt gaps modifies the wake, which changes drag and stability.

**Momentum conservation (incompressible Navier–Stokes)** *(standard form; the report shows it as an image)*:

$$\rho\left(\frac{\partial\mathbf{u}}{\partial t} + (\mathbf{u}\cdot\nabla)\mathbf{u}\right) = -\nabla p + \mu\,\nabla^{2}\mathbf{u} + \rho\,\mathbf{g}, \qquad \nabla\cdot\mathbf{u}=0.$$

The terms are inertia, pressure gradient, viscous diffusion and gravity. These equations govern flow separation, vortex shedding and turbulence, and are solved numerically with CFD. In the report's discussion the skirt gaps act like small nozzles whose jets rebalance pressure and help keep the cork-first orientation.

Ratio of the inertial to viscous terms is exactly the Reynolds number above, which is why Re controls the flow regime.

## 6. Pressure Distribution and Complex Potential

The report compares feather, plastic and gapless (solid) shuttlecocks by their **pressure coefficient**

$$C_p = \frac{p - p_\infty}{\tfrac12\rho V^2}$$

and by complex-analysis arguments for 2D idealised flow.

**Complex potential.** For 2D, incompressible, irrotational flow,

$$F(z) = \phi + i\psi, \qquad z = x+iy,$$

where $\phi$ is the velocity potential and $\psi$ the stream function. $F$ is analytic away from singularities, $\phi$ and $\psi$ satisfy the Cauchy–Riemann equations (so both are harmonic), and the velocity is recovered from $\dfrac{dF}{dz} = u - iv$. By Bernoulli, $C_p = 1 - \left(|\mathbf{u}|/V\right)^2$ in this ideal setting.

**How the report uses it**

| Design | Mathematical picture (from the report) | Resulting $C_p$ | Consequence |
|--------|-----------------------------------------|-----------------|-------------|
| **Feather** | Gaps act as periodic discontinuities, like singularities of $F(z)$; vortex shedding appears as branch cuts | Large peaks and troughs, low pressure behind each gap | Highest drag, strong stabilising spin, straightest flight |
| **Plastic** | Regular vane pattern modelled with conformal mapping | Smoother, moderately negative on the leeward side | Lower drag, weaker spin, some wobble |
| **Solid (gapless)** | Classic potential flow around a hemispherical body; $F(z)$ analytic on the whole domain | Smooth: maximum at the stagnation point, gradual decrease | Lowest drag, no vorticity, no stabilising spin, unstable |

**Background for these arguments** *(extension)*

- Building blocks of 2D potential flow: uniform stream $F = Vz$, source $F = \frac{m}{2\pi}\ln z$, point vortex $F = -\frac{i\Gamma}{2\pi}\ln z$. The logarithm is multivalued, so a vortex carries a branch cut, which is the link to the report's "branch cut" language.
- Conformal maps (angle-preserving analytic maps) transform a simple flow, such as flow past a circle $F = V(z + a^2/z)$ with $C_p = 1 - 4\sin^2\theta$, into flow past a more complicated body.
- **Limit of the model:** steady potential flow predicts *zero drag* (d'Alembert's paradox). Real drag comes from viscosity, separation and the wake, which is why the potential-flow picture is used here qualitatively and the full Navier–Stokes equations are needed for quantitative results.

## 7. Summary of Model Comparisons

| Quantity | Feather | Plastic | Solid |
|----------|---------|---------|-------|
| Drag | Highest | Moderate | Lowest |
| Speed | Lowest | Moderate | Highest |
| Pressure variation ($C_p$) | Large | Moderate | Minimal |
| Vortices / spin | Strong | Weak | None |
| Stability | Best | Wobbles | Unstable |

Overall conclusion of the report: the design trades speed for control, since higher drag and vorticity are what keep the shuttlecock stable.

## 8. Repository Contents

```
.
├── README.md
├── Project_Report.pdf     # Full written report
└── Project_PDF.pdf        # Presentation slides
```

The report also contains historical sections on the evolution of shuttlecocks (1840–1993) and racquets (1909–2024), which are not covered in this math-focused README.

## 9. References

1. Kitta, S., Hasegawa, H., Murakami, M., & Obayashi, S. (2011). Aerodynamic properties of a shuttlecock with spin at high Reynolds number. *Procedia Engineering, 13*, 271–277. https://doi.org/10.1016/j.proeng.2011.05.084
2. Hart, B., & Potts, J. R. (2020). Numerical investigation of the flow around a feather shuttlecock with rotation. *Proceedings, 49*(1), 28. https://doi.org/10.3390/proceedings2020049028
3. Mittal, S. (n.d.). *Sports Aerodynamics: Cricket Ball & Badminton Shuttlecock.* IIT Kanpur.
amics-of-a-Shuttlecock-The-Mathematical-Model
