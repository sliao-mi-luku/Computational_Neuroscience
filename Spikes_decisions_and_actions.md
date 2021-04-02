# Spikes, decisions, and actions
## dynamical foundations of neuroscience

*Hugh R. Wilson*

---

**Contents in Brief**

Ch1. Introduction\
Ch2. First order linear differential equations\
Ch3. Two-dimensional systems and state space\
Ch4. Higher dimensional linear systems\
Ch5. Approximation and simulation\
Ch6. Nonlinear neurodynamics and bifurcations\
Ch7. Computation by excitatory and inhibitory networks\
Ch8. Nonlinear oscillations\
Ch9. Action potentials and limit cycles\
Ch10. Neural adaptation and bursting\
Ch11. Neural chaos\
Ch12. Synapses and synchrony\
Ch13. Swimming and traveling waves\
Ch14. Lyapunic functions and memory\
Ch15. Diffusion and dendrites\
Ch16. Nonlinear dynamics and brain function


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
  - ion channel conductance depends on the membrane potential
  - 
- Two-dimensional Rinzel approximation

- Noisy neurons
  - noise can improve the performance of a nonlinear system
  - noise added to the stimulus increases the probability of firing predominantly when the stimulus sinusoid is near its peak phase
  - subthreshold noise can increase the sensitivity to prediodic sensory stimulation
  - stochastic resonance
  - the nature of the stimulus is encoded into the interspike intervals (Poisson process) in the response
  - 

**10. Neural adaptation and bursting**

- Spike frequency adaptation
  - RS (regular-spiking) neurons
  - inclusion of an additional K+ current (I_AHP current), with a 20-times slower time constant than the recovery variable
  - `dV/dt = -{Na+ term} - {Recovery term} - 13*H(V)*(V+0.95) + {I_input}`
  - `dH/dt = (1/99) * {-H + 11*(V+0.754)*(V+0.69)}`

- Neural bursting and hysteresis

- Calcium currents and parabolic bursting
  - incorporating a transient inward Ca2+ current (I_T) + hyperpolarizing Ca2+ current (I_AHP)
  - `dV/dt = - {Na+ term} - {Recovery term} - 1.93X*(1-0.5C)*(V-1.4) - 3.25C*(V+0.95)`
    - X: Ca2+ conductance (I_T term). Eeq = +140 mV. tau_X = 30 ms. dX/dt = (1/30)*(-X + function(V^2))
    - C: Ca2+-modulated conductance of an additional K+ channel. Eeq = -95 mV. dC/dt = (1/100)*(-C + 3X) independent of V\
    - No external input. Bursting is driven by the slow increasing I_T -> endogenous burster
    - pacemaker
  - parabolic bursting: spiking rate at the beginning/end of a burst is slower than during the middle of the burst

- Neocortical bursting
  - mouse somatosensory cortex
  - "chattering cells" in cat visual cortex
  - not endogeneous: need current injection
  - spike height decreases after the first spike in a burst

**11. Neural chaos**

- chaos
  - (1) trajectories are aperiodic and remain within a bounded volume, without approaching any steady state
  - (2) sensitivity to initial conditions. arbitrary small change in the i.c. will lead to exponential uncertainty in the future
  - (3) chaos cannot exist in a two-dimensional system

- tests to differentiate limit cycles, quasiperiodicity, chaos, and noise
  - Fourier power spectrum
  - first return map
  - Poincare section
  - Lyapunov exponent

- Neural chaos in motor control
  - prey escaping
  - creativity
  - 

**12. Synapse and synchrony**

- Phase oscillator
  - only the phase of each oscillator need to be considered when the coupling is weak
  - the amplitude and the waveform of each limit cycle will be largely unaffected under weak coupling
  - two coupled oscillators

- Reciprocal inhibition
  - Clione swimming
  - anti-phase oscillation
  - postinhibitory rebound
    - after each neuron spike, an hyperpolarizing IPSP in the other cell results in postinhibitory rebound
    - The other cell generates a spike
    - IPSP must be brief (short) and strong

- Inhibitory synchrony
  - synaptic conductance change persists over time
  - postsynaptic effect `P(t) = (k/tau_syn^2)*t*exp(-t/tau_syn)`
  - reciprocal inhibitory connection:
    - short tau_syn -> antiphase
    - long tau_syn -> synchrony
  - reciprocal excitatory connection:
    - short tau_syn -> synchrony
    - long tau_syn -> antiphase

- Thalamic synchronization during deep sleep
  - 

**13. Swimming and traveling waves**

- Swimming of lamprey
  - Central pattern generator in each spinal cord segment
  - Coupled phase oscillators
  - The job of the brain:
    - send a constant command to all segments
    - send a slightly greater command to the first segment to swim forward,
    - or send a slightly greater command to the last segment to swim backward
  - side note:
    - connection between non-adjacent segments help to produce traveling waves with a wavelength equal to the body length

- Quadeuped locomotion
  - the model
    - we only need to write the equations of the left and right forelimbs, because hind leg is always out of phase of the ipsilateral fore leg
    - 
  - the difference between b (left-right coupling stength) and c (diagonal coupling) will determine trotting or galloping, and which one is stable

- Swimming of Tritonia
  - neuron types
    - DSI: dorsal swim interneuron, excites motoneurons for dorsal flexion
    - C2: C2 neuron
    - VSI: ventral swim interneuron, excites motoneurons for ventral flexion
  - the phenomemon
    - each rhythmic activity consists of 4-7 cycles
    - activation of DSI -> C2 -> VSI
  - the model
    - DSI (x3): recurrent excitatory, with I_AHP current, excite C2, inhibit VSIs
    - C2 (x1): with I_AHP current, excites VSI
    - VSI (x2): recurrent excitatory, with I_A current, inhibit DSIs, inhibit C2
  - explanation
    - DSI-DSI synaptic time constant is large (~320 ms)
    - rhythmic activity ends after several cycles because of the slow increasing hyperpolarization by I_AHP (tau_AHP = 1250 ms)

**14. Lyapunov functions and memory**

- limitation of linearized stability analysis
  - not work in the case where the eigenvalues are pure imaginary
  - doesn't tell the range of initial conditions from which the trajectory will decay to the asymptotically steady state

- state function
  - scalar function (U) of variables that has continuous partial derivatives throughout the state space
  - U is positive definite in a region R surrounding an internal singularity x0 if
    - U(x0) = 0
    - U(x) > 0 in R if x != x0
    - mathematical valley around the signularity

- **Lyapunov theorem**
  - domain of attraction/domain of asymptotic stability
  - Lyapunov functions are not unique for any particular dynamical system
  - All asymptotically stable singular points have associated Lyapunov functions
  - the existence of a Lyapunov function is both necessary and sufficient for asymptotic stability

- construct a Lyapunov function
  - given equation dx/dt = F(x, y), dy/dt = G(x, y)
  - F(x, y) = 0, G(x, y) = 0 are the isoclines
  - 

- Constant of motion
  - if `dx/dt = A(x)*B(y)`, `dy/dt = C(x)*D(y)`
  - then U(x,y) = Integral_over_y[B(y)/D(y)] - Integral_over_x[C(x)/A(x)] (as long as the integral can be evaluated)
  - the corresponding oscillation is called conservative oscillation
  - any trajectory starting with (x0, y0) will evolve forever along the locus where U = U(x0, y0) = constant

- Long-term memory
  - hippocampus: stores and consolidates episodic memory -> transfer to higher cortical areas
  - Hebb's learning rule
    - weight of the synaptic connection `w = k*R_pre*R_post`
    - event A: presynaptic neuron releases glutamate
    - event B: postsynaptic neuron depolarizes dendrites to remove Mg2+ which are blocking the NMDA receptor
    - NMDA receptor can only be activated if events A and B occur within 100-200 ms
  - hippocampus CA3 model:
    - a 16x16 grid pyramidal cells (256 in total), 1 inhibitory interneurons
    - Ri: the firing rate of the i-th pyramidal cell (i = 1~256)
    - M: the maximum firing rate of a pyramidal cell
    - k: maximum synaptic strength achievable between a pair of pyramidal cells
    - w_ij = synaptic strength onto neuron_j by neuron_i
    - `w_ij = w_ji = k*H(Ri-0.5M)*H(Rj-0.5M)`
    - each pyramidal cell projects to all other 255 pyramidal cells
    - inhibitory neuron inhibits all 256 pyramidal cells
    - dynamical equations:
      - `tau * dRi/dt = -Ri + NakaRushton(stimulus = sum(w_ij*Rj)-0.1*G, max_rate = 200, sigma = 10)`
      - `tau * dG/dt = -G + g*sum(Ri)`
    - associative network: stimulation by a portion of any previously learned pattern will cause the network to recall the entire pattern


  - Dynamic temporal memories

**15. Diffusion and dendrites**

- Cable equation
  - D: length constant (proportional to sqrt(r), r = radius of the axon/dendrite)

- Passive dendritic potentials
  - mathematically we can treat the length of the dentrites to be infinity because it's >> D
  - 










