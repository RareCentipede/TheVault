#academics #ics

Machine learning is the study of computer algorithms that improve automatically through experience. #definition #ml

## ML into the control loop
1. Model learning for control (non-linear identification)
	1. The model is (pre-) learned when needed
	2. If the error is small, then the model is good, and it can be used as a base for standard control design techniques.
![[Pasted image 20240325155538.png]]
2. Direct control learning
	1. The controller learns how to drive the error signal to zero, or to maximize the fitness/reward.
		1. Learning feedforward action
		2. Learning afeedback controller
![[Pasted image 20240325155627.png]]
## Learning the model
Consider model learning when the *state* is measureable.

### Discrete-time
- Data generation, initial condition
	- All relevant portions of the state space must be explored
	- Can be done by varying the initial condition and let the system evolve
- Continuous time
	- Often only a set of measurements in time and the associated control inputs are known.
		- x is not known and hidden by the output function

## Non-linear systems and control theory
- Dynamical system
	- A system whose state evolves with time, governed by a set of rules that specifies the state of the system for either discrete or continuous values.
	- Discrete-time evolution
		- Usually described by a system of algebraic equations (map)
	- Continuous-time evolution
		- Usually described by a system of differential equations
	- Block operators view ![[Pasted image 20240325161432.png]]
		- $u:$ manipulated variable (control input)
		- $x:$ state, which is the minimum amount of information necessary to describe the instantaneous behavior of the system (and to predict its state at the next isntant)
		- $y:$ output
	- Continuous-Time affine in control
		- The evolution $x(t) \in X$  in time under the excitation $u(t) \in U$ for the dynamical system $< X, Y, U, f, g, h >$  is the solution of the following set of ODEs (governing equations)
			- $\dot{x} = f(x) + g(x) u$ 
		- Evolution of the output $y(t) \in Y$
			- $y = h(x, u)$
- To obtain models
	1. Physical modeling
		- First principles -> differential equations
	2. Data-driven
		- System identification/machine learning
		- Measure input-output data
		- Postulate model structure
		- Estimate model parameters from data
- Equilibrium
	- A state that the system will not move away from if left undistrubed
- Stability of an equilibrium
	- A characterization of behavior outside the equilibrium
	- The equilibrium point $x$ is
		- stable if, for each $\epsilon > 0$  there is $\delta = \delta(\epsilon) > 0$   such that
			- $||x(0)|| < \delta \rightarrow ||x(t)|| < \epsilon, \forall t \geq 0$ 
		- Asymptotically stable if it is stable and $\delta$ can be chosen such that$$||x(0)|| < \delta \rightarrow \lim_{t \rightarrow \infty} x(t) = 0$$
## Lyapunov analysis
1. Select a Lyapunov Candidate
2. Look for the time derivative
3. Check the sign of $\dot{V}$
## Continuous-time linear systems
- A dynamical system is linear if $f(x) + g(x)u$ and $h(x, u)$ are linear simultaneously w.r.t $x$ and $u$
- The system has a single equilibrium in $\hat{x} = 0$ 
	- or infinite equilibria if $det(A) = 0$
- If $\hat{x}$ is asymptotically stable, then it is globally AS
- Easy to check stability
	- AS iff all eigenvalues of A have real part smaller than 0
- Can approximate non-linear systems with linear ones
- Stability of linear approximation implies stability of the exact non-linear system
- The vice versa does not hold necessarily

## Discrete time systems
- Time is measured using integers rather than real numbers
- Stability
	- Eigenvalue of Ad must have norm smaller than 1

## Feedforward control
**Pros**
- Does not risk to destabilize stable systems
- It is an essential component of control by linearization
- Simple solution to obtain good performance if the system is "stable enough"
**Cons**
- Cannot stabilize unstable systems
- Cannot suppresss the effect of disturbances
- Sensitive to uncertainty in the model

## Feedback control
**Pros**
- Can stabilize unstable systems
- Can suppress the effect of disturbances
- May be robust to uncertainty in the model
**Cons**
- Can destabilize stable systems
- There is no straightforward way of prescribing performance
- May be complex to design

## Model-free and model-based
- Controller is model-free if it does not require the availability of a model to be formulated
- Controller is model-based if it does require the (partial) knowledge of a dynamical model of the system.

## [[Equations of motion of mechanical system]]
**Fully actuated mechanical system**
- $M(q)\ddot{q} + C(q, \dot{q})\dot{q} + G(q) + D(q)\dot{q} = \tau$
**PD + Gravity compensation**
- $\tau = K_p(\hat{q} - q) + K_d(\hat{\dot{q}} - \dot{q}) + G(q)$

# [[Model based control]]