# Spikes, decisions, and actions
## dynamical foundations of neuroscience
*by Hugh R. Wilson*

---

### Contents

1. Introduction
2. First order linear differential equations
3. Two-dimensional systems and state space
4. Higher dimensional linear systems
5. Approximation and simulation
6. Nonlinear neurodynamics and bifurcations
7. Computation by excitatory and inhibitory networks
8. Nonlinear oscillations
9. Action potentials and limit cycles
10. Neural adaptation and bursting
11. Neural chaos
12. Synapses and synchrony
13. Swimming and traveling waves
14. Lyapunic functions and memory
15. Diffusion and dendrites
16. Nonlinear dynamics and brain function


### Lecture Notes

**2. First order linear differential equations**

> dV/dt = -(1/tau){g_L(V-E_L) + g_e(V-E_e) + g_i(V-E_i)}

- Shunting effect of GABAa synapses: they short circuit the depolarizing current produced by EPSPs.
- Nonlinear interaction between EPSPs and IPSPs. Only when these synapses are far apart can make the effect subtractive.

**3. Two-dimensional systems and state space**

- Two-component system

- Solving linear second order differential equations `dX/dt = AX + B`
  - find steady state Xeq : `AXeq + B = 0`
  - obtain new equations `dX'/dt = AX'`
  - find the characteristic equation `det|A-lambda*I| = 0`, solve for `lambda_1` and `lambda_2` (eigenvalues)
  - solve eigenvectors `V_1 and V_2` by `A*V_1 = lambda_1*V_1` and `A*V_2 = lambda_2*V_2`
  - solution has the form `X = X' + Xeq = a V_1 + b V_2 + Xeq`
  - use initial conditions to solve `a` and `b`
  
- Negative feedback in the retina
  - cones stimulate horizontal cells
  - horizontal cells inhibit cones
  - experiments: stimulating cones by a step function of luminance -> overshoot -> slight undershoot -> equilibrium
  - the model (C:cone, H:horizontal cell, L:light-induced stimulus, k:gain of the inhibitory feedback):
      - dC/dt = {1/(tau_C)} * (- C - kH + L)
      - dH/dt = {1/(tau_H)} * (- H + C)
      
- Stability
  - asymptotically stable: all trajectories starting within a region containing the equilibrium point will decay to that point as time -> infinity
  - unstable: at least 1 trajectory starting within a region containing the equilibrium will leave the region permanently
  - stable/neutrally stable: nearby trajectories will remain nearby as time -> infinity, but will not approach asymptotically
  
- Traejectories in the state space <-> solutions to the 2nd order differential equation
  - **spiral point**: eigenvalues are complex conjugate pair. If real(eigenvalue) < 0 -> asymptotically sable
  - **node**: eigenvalues are read and have the same sign.
    - asymptotically stable node: both eigenvalues are negative
    - unstable node: both eigenvalues are positive
  - **saddle point**: eigenvalues are real but have opposite signs
  - **center**: eigencalues are pure imaginary.
  - **critical damping**: two eigenvalues are equal.
  
- Critical damping and muscle contraction
  - `x" + 2ax' + a^2(x-x0) = 0`
  - `x(t) = A*exp(-at) + B*t*exp(-at) + x0`

**4. Higher dimensional systems**

- Routh-Hurwitz criterion
- Routh-Hurwitz criterion for oscillations
- Respiration
- Feedback with delays
  - delay increases the dimensionality of a dynamical system
  - increased time delays may cause dysfunctions (ex. sclerosis)
  
**5. Approximation and simulation**

- Euler's method
  - `x(t+dt) ~ x(t) + dt*(dx/dt)`
- Runge-Kutta
