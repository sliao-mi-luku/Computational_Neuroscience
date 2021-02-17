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

- Naka-Rushton function
  - gives the **spike rate** (R) as a function of the **stimulus intensity** (S)
  - if S <= 0: R(S) = 0
  - if S > 0: R(S) = (M\*S^N) / (sigma^N + S^N)
  - M: maximum spike rate, sigma: semisaturation constant 

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
  - Taylor expansion keeping only the first order
  - `x(t+dt) ~ x(t) + dt*(dx/dt)`
  - cons: always produces an unstable spiral solution around a steady state (center)
  
- Runge-Kutta
  - higher order in Taylor expansion
  - 4th order Runge-Kutta: `x(t+dt) ~ x(t) + (dt/6)*(K1 + 2*K_2 + 2*K_3 + K_4)`

- Error ratios
  - Euler's method: 1
  - 2nd order Runge-Kutta: 1/3
  - 4th order Runge-Kutta: 1/15
  
**6. Nonlinear neurodynamics and bifurcations**

- Negative feedback in a divisive gain control
  - B: bipolar cell, A: amacrine cell, L: light level
  - `dB/dt = (1/tau_B)*{-B + L/(A+1)}`
  - `dA/dt = (1/tau_A)*{-A + 2B}`

- Stability of nonlinear system
  - given `dX/dt = F(X)`
  - find the equilibrium state `Xeq`
  - calculate the **Jacobian matrix** of F **at Xeq**
    - if all eigenvalues have negative real parts -> asymptotically stable
    - if at least 1 eigenvalue has positive real part -> unstable
    - if at least 1 eigenvalue is 0 -> Jacobian is not enough to say
    - if any eigenvalue pair is pure imaginary -> Jacobian is not enough to say
  - 
- Mutual excitation in short-tem memory
  - delayed response task
  - prefrontal neurons
  - Naka Rushton function: spike_rate = NakaRushton(stimulus)
  - `dA/dt = (1/tau)*(-A + NakaRushton(3*B))`
  - `dB/dt = (1/tau)*(-B + NakaRushton(3*A))`
  - plotting isoclines reveals **multiple equilibria** where `dA/dt = dB/dt = 0`
  - *hysteresis*: present state not only depends on the present stimulus but also on the history of stimulation
  - short-term memory comes from the phenomenon that the system remains in a asymptotically stable equilibrium until the stimulus jumps and moves the system to another state 
  - adaptation: introducing additional variables to account for an increase in the constant `sigma` in the Naka-Rushton function
  
- Mutual inhibition in neural decision making
  - winner-take-all
  - 2 asymptotically stable nodes separated by a unstable saddle point
  - hystereis: once a neuron prevails, the other neuron needs much more stimulus to override the winner
  
**7. Computation by excitory and inhibitory networks**

- Neural decision based on sensory evidence
  - visual search experiment with 1 target (T) and N distractors (D)
  - Naka-Rushton function for stimulus-response relation
  - response = NakaRushton(stimulus) = max_response\*stimulus^2 / (sigma^2 + stimulus^2) if stimulus > 0 else 0
  - `dT/dt = (1/tau) * (-T + NakaRushton(input_of_evidence_to_T - k*N*D)`
  - `dD/dt = (1/tau) * (-D + NakaRushton(input_of_evidence_to_D - k*(N-1)*D - k*T)`
  - exeperiments showed as the number of distractors (N) increases -> response time (latency) increase

- Wilson-Cowan cortical dynamics
  - all forms of interconnections: E->E, E->I, I->E, I->I
  - 

**8. Nonlinear oscillations**

- Biological rhythms evolved to be inherently nonlinear so that the rhythm can be immune to the noise.

- *limit cycles*
  - definition: oscillatory trajectory is a limit cycle if all trajectories in a sufficiently small region enclosing that region are spirals
  - a lmiit cycle is stable if neighboring trajectory spirals toward it as t -> inf
  - a limit cycle is unstable if neighboring trajectory spirals away from it as t -> inf
  - theorem (2-dimensional system)
    - if a limit cycle exists in a autonomous (trajectory can't cross itself) system, it must surround at least 1 equilibrium point
    - if it encloses only 1 equilibrea -> node, spiral point, or center. It can not be surrounding a saddle point
    - if it encloses multiple equilibrea -> n(nodes) + n(spiral points) + n(centers) - n(saddle points) = 1
  - Pointcare-Bendixon theorem (2-dimensional system)
    - an annular region must contain at least 1 limit cycle if:
    - (1) the annular region dosn't not contain equilibrium points, and
    - (2) all trajectories crossing the boundary of the region enter it

- Wilson-Cowan network oscillator
  - cortex, where 25% are inbihitory GABA neurons and rest are excitatory glutamate neurons
  - the model: 3 excitatory neurons and 1 inhibitory neuron with:
    - excitatory neurons mutually excite each other
    - all excitatory neurons project to the inhibitory neuron
    - the inhibitory neurons projects to all 3 excitatory neurons
    - all excitatory neurons receive external stimulation

- FitzHugh-Naguma equations
- 
- Hopf bifurcation theorem (>=2 dimensional system)
  - given the system `dX/dt = F(X, b)`, where `b` is a parameter
  - given Xeq an equilibrium point
  - if there exist `a` such that:
    - (1) when b < a, Xeq is asymptotically stable
    - (2) when b = a, the system has a pair of pure imaginary eigenvalues (+/-)iw, and all other eigenvalues have negative real parts
    - (3) when b > a, Xeq is unstable
  - then
    - the system has an asymptotically stable limit cycle over a range b > a, or
    - the system has an unstable limit cycle over a range b < a
    - near b = a, the oscillatio will be ~ w/2*pi

- Delayed negative feedback
- Competitive networks with adaptation

**9. Action potentials and limit cycles**

- Hodgkin-Huxley equations

**10. Neural adaptation and bursting**

**11. Neural chaos**

**12. Synapse and synchrony**

**13. Swimming and traveling waves**

**14. **
