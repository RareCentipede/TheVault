# Temporal unrolling
- An alternative to vanilla regression loss when learning dynamical systems
	- Especiall in continuous time
- Train a neural network to approximate the behavior of a non-linear dynamical system. Assume that the state can be measured.
- Time evolution of the learning dynamics $$\bar{x}(t) + \int^T_0NN_w$$
# Learning the model from outputs
- Input is hidden by the output function.
- Reasons:
	- Natural representation of the state is clear, but there is no collocated sensors
	- No idea about the nature of the underlying state of the system
- Learn the dynamics of systems when it is not possible to directly measure or even characterize the state
- A non-linear time-discrete system: $$x_{k+1} = f(x_k, u_k), \quad y_k = h(x_k)$$
	- When $y_k$ is an admissible state representation of the system, meaning it carries all the neccessary information on the system behavior, it can be used as a system state and directly learn $f_y$ in $$y_{k+1} = f_y(y_k, u_k)$$

## Delayed outputs
- $h$ might not always be invertible, since the state $x$ could contain both the configurations of the system and the associated time derivatives, and only the former can usually be measured.
	- Hence, $h: \mathbb{R}^{2n} \rightarrow \mathbb{R}^n$ and cannot be inverted $(2n < n$).
- Add delayed outputs

# [[Recurrent Neural Networks]]
# [[Echo State Network]]
