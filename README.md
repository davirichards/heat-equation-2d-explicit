# heat-equation-2d-explicit

**Finite difference simulation of 2D heat diffusion: explicit FTCS scheme with Dirichlet boundary conditions**

## What it does

Solves the two-dimensional heat diffusion equation:

$$\frac{\partial u}{\partial t} = \alpha \left( \frac{\partial^2 u}{\partial x^2} + \frac{\partial^2 u}{\partial y^2} \right)$$

over a rectangular domain [0, Lx] × [0, Ly] using the **Forward Time Centered Space (FTCS)** explicit finite difference scheme. Specifically:

- Discretizes spatial domain: Nx × Ny grid points
- Discretizes temporal domain: Nt time steps with step size ht
- Initial condition: u(x,y,0) = 200 K everywhere, with u = 400 K inside a circular hot spot
- Boundary conditions: Dirichlet (u = 200 K on all boundaries, constant in time)
- Time integration: Explicit FTCS method

## Why this problem matters

Heat diffusion is a fundamental PDE in physics, materials science, and engineering. The FTCS scheme is the simplest explicit method but has **strict stability requirements** (CFL condition). This problem demonstrates:

- How stability constraints limit step size for explicit methods
- Trade-off between accuracy and computational cost
- Why implicit methods become necessary for larger time steps
- Smooth heat dissipation from localized hot source

## Method

| Component | Value |
|-----------|-------|
| **Domain** | 2.0 × 1.0 |
| **Grid** | 200 × 100 nodes |
| **Thermal diffusivity** | α = 0.0014 |
| **Time domain** | 0 to 2.6 seconds |
| **Stability criterion** | sx, sy < 0.25 (CFL satisfied) |

**Discrete scheme:**
$$u_{j,i}^{n+1} = \sigma_x u_{j,i+1}^n + \sigma_x u_{j,i-1}^n + \sigma_y u_{j+1,i}^n + \sigma_y u_{j-1,i}^n + (1-2\sigma_x-2\sigma_y) u_{j,i}^n$$

Where σx = αht/hx² and σy = αht/hy²

## Key outputs

Temperature field snapshots at t=0 (initial condition) and t=2.6 (final state), showing:
- Heat propagation from initial circular hot spot
- Diffusion toward steady-state (200 K everywhere)
- Spatial smoothing enforced by diffusion operator

## Tech stack

- **Python** — Core implementation
- **NumPy** — Array operations and grid computation
- **Matplotlib** — Visualization of temperature fields
- **Animation API** — Temporal evolution rendering

## Installation & usage

```bash
pip install numpy matplotlib
python heat_equation_2d.py
```

Outputs visualization of temperature distribution at multiple time snapshots via matplotlib colormap rendering.

## Stability & performance

| Grid Size | Time Steps | Computation (approx) |
|-----------|-----------|----------------------|
| 100×50 | 1000 | < 1 sec |
| 200×100 | 5000 | 5-10 sec |
| 400×200 | 10000 | 30-60 sec |

FTCS stability requirement: σ_max = max(σx, σy) ≤ 0.25 (satisfied by automatic ht selection)

## Connection to the field

This problem bridges classical PDE theory and modern computational methods. Applications span: thermal engineering (heat sinks, microelectronics), materials processing, geophysics (temperature diffusion), and atmospheric modeling. The explicit scheme illustrates fundamental computational limits motivating development of implicit solvers (Backward Euler, Crank-Nicolson).
