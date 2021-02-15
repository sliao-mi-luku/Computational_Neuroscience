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
