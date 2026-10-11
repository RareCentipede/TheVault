# Intro
- Techniques for devising controllers from the possibly partial or local knowledge of the system model.

# Feedback linearization
- Consider a non-linear time continuous affine in control model, then differentiating the output until the input appears yields the normal form.
- The control action yields the linear closed loop visible dynamics
- Any linear closed loop controller can be used to shape the closed loop behavior
- **Pros:**
	- Very general and theoretically sound technique
- **Cons:**
	- Not robust, can be used only if the system is minimum phase

# Feedforward control for output tracking
- Find a feedforward action that realizes an desired evolution in nominal conditions![[Pasted image 20240410182818.png]]

# Feedforward control for state regulation
- Easier to look for the constant control action that renders $\bar{x}$ a (possibly unstable) equilibrium for the system.

# Control by _standard linearization:_ FF + FB
- If the feedforward action is _good enough_, then the non-linear system can be assumed to be evolving _close to_ the desired trajectory or equilibrium.
- In this case, the non-linear system can be linearized around the equilibrium (or trajectory) obtaining a local linear description $$\delta \dot{x} = A\delta x + B\delta u$$
- Classic linear techniques can then be used to design an effective feedback controller
![[Pasted image 20240410184653.png]]