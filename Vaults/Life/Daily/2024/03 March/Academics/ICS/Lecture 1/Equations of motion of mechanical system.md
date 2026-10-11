**Fully actuated mechanical system**
- $M(q)\ddot{q} + C(q, \dot{q})\dot{q} + G(q) + D(q)\dot{q} = \tau$
**PD + Gravity compensation**
- $\tau = K_p(\hat{q} - q) + K_d(\hat{\dot{q}} - \dot{q}) + G(q)$
**PD + Feedforward**
- $\tau = K_p(\bar{q}-q) + K_d(\dot{\bar{q}}-\bar{q}) + M(\bar{q})\ddot{\bar{q}}) + C(\bar{q}, \dot{\bar{q}})\dot{\bar{q}} + G(\bar{q}) + D(\bar{q})\dot{\bar{q}}$
- From linearizing the system around the desired trajectory
- Can also be analyzed theoretically in the fully non-linear setting, showing that the tracking error will be bounded if the desired trajectory is slow enough and the control gains are high enough.
**PD+**
- Similar to PD+FF but all the terms are calculated using the current $q$ and its derivative, rather than the reference.
- Can achieve imporved performance and provable steady state null error
- However, C needs to be calculated with Christoffel symbols which is inefficient
**Computed Torque (FB-Linearization MIMO)**
- Everything evaluated in the current configuration and velocity
	- Acceleration not part of the state
- Strongly improved performance in the nominal case
- The only controller ensuring exponential convergence
- Requires very good knowledge of the model