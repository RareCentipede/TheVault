# Weeks 1-3
1. What has been the original motivation behind artificial neural networks?
	- To imitate biological neural networks for its learning and adaptive capabilities and parallel information processing, where no prior knowledge is present and to overcome complex problems with pattern recognition and image processing.
2. Block diagram of an artificial neuron![[Pasted image 20240408153856.png]]
3. Give three examples of activation functions
	- Maps the activation $z \in (-\infty, \infty)$ onto some interval.
	- ReLU (Rectified Linear Unit)
	- Sigmoid
	- tanh
4. Explain training of a neural network
	- Make predictions, record the loss, backpropagate to optimize the weights such that the error between the predictions and output are minimized, and repeat until the maximum number of steps is reached.
	- Training adjusts the parameters of the network to minimize an error cost function. It is the adaptation of weights in a network such that a certain goal is achieved. By training, the network learns to approximate a certain function from examples of input output data pairs.
5. What are the steps of the backpropagation algorithm?
	- Compute the error between the prediction and ground truth label.
	- DIfferentiate the weights with respect to the error and move backwards until the input layer is reached.
	- Optimize the weights based on the gradients.
6. Use the backpropagation rule to derive the derivative of the squared error cost with respect to hte weights of an output neuron with an activation function $\sigma$
7. Practical linear regression problem
	a. Explain why we are adding the second term to the cost function.
		To keep the weights small so that the model is not overly complex, which reduces the chances of overfitting.
	b. Write down the gradient of the cost function.
	c. Write downw the update rule for gradient descent with regularization.
	d. Use the result from (c) to evaluate the difference in updates for $\lambda = 1/10$ compared to $\lambda = 1/2$
9. Neural networks have activation functions. Sum of basis functions is linear in the parameters and input weights are unity and has only one layer.
10.  Dynamic system approximator 
	![[Pasted image 20240410171601.png]]
		- $\Delta$ is the delay operator.
	- Cost function $$J = (\hat{y}[k+1] - y[k+1])^2$$
	- Can use first or second-order gradient descent method.
11. Inverse model of a feedforward control scheme.![[Pasted image 20240412153346.png]]
	- **Objective:**
		- Compute the control input of the current state, such that the system's output at the next sampling instant is equal to the desired (reference) output.
		- Can be achieved if the process model can be inverted according to $$u(k) = f^{-1}(x(k), r(k+1))$$ where the state can be updated by using the output of the model.
	- The reference-shaping filter generats the desired dynamics in order to avoid peaks in the control action for step-wise references.
	- If a model of the process is unavailable, the direct model can be trained by collecting input-output data, then train the inverse using $(y, Model(u))$
12. Explain the main concept of Model Predictive Control
	- A model is used to predict the process of the dynamics. An optimization problem with the objective to follow the reference trajectory or to reach a destination is subjected to constraints, which can be velocity and acceleration limits, so the predicted trajectory is physically feasible, as well as obstacle avoidance constraints.
	- **Accurate answer**
		- In predictive control a model is used to predict the process output at future discrete time instants over some prediction horizon. The sequence of future control actions is computed by minimizing an objective function which penalized the difference between the predicted output and the desired output (the reference). Only the first control action of the obtained sequence is applied to the process, the horizon is moved one step forward and the optimization is repeated. Usually, the following quadratic cost function is applied: $$J = \sum^{H_p}_{i=1} ||r(k+i) - \hat{y}(k+i)||^2_{P_i} + \sum^{H_c}_{i=1}||\Delta u(k+i-1)||^2_{Q_i}$$
			- The first term penalizes the differences between the process output around the reference, while the second is a penalty on the control effort. $\bf{P_i}$ and $\bf{Q_i}$ are positive definite weighting matrices that specify the relative importance of the two terms.
	- **Machine learning application example**
		- Learn a direct model of the system and use it to predict the response of the system while performing the numeric optimization.
13. 
	1. 
		- ReLU is not invertible for all inputs less or equal to zero.
	2. 
16. 
	1. Depends on the value of $r$. For large $r$, it is convenient to use a neural network, otherwise, a sum of basis function is more convenient.
		1. The error of a neural network prediction decreases asymptotically with the number $h$ of neurons in the hidden layer: $\mathcal{O}(1/h)$
		2. The error of a sum of basis functions decreases asymptotically as $\mathcal{O} (1/H^{2/p})$, where $h$ is the number of basis functions and $p$ the number of inputs.
	2. 
		a. 
			Take basis functions from a truncated basis of the functional space to which $f$ belongs. For $\mathbb{R}^2 \rightarrow \mathbb{R}$, a base are the two-dimensional monomials of any order. A truncated base is therefore $$\phi(p, \dot{p}) = [p, \dot{p}, p^2, p\dot{p}, \dot{p}^2, p^3, p^2\dot{p}, p\dot{p}^2, \dot{p}^3, p^4, p^3\dot{p}, p^2\dot{p}^2, p\dot{p}^3, \dot{p}^4]^T$$ which corresponds to polynomials in $p$ and $\dot{p}$ up to the $4^{th}$ order.
		b. 
			To build expert intuition, interpret the electron as a point with acceleration $\ddot{p}$ subject to repulsive forces that are configuration $p$ dependent, and to some form of dissipation which will depend on $\dot{p}$.
			Alternatively, rely on the fact that the crystal is periodic, as its structure repeats every $L$: $$\phi_i(p) = sin(2(i-1)\pi p/L)$$
	3. Use Lagrangian neural network, assume the repulsive forces are poential forces.
17. How to create the reservior in an echo state network?
			Created by initializing a randomly connected network of neurons, where a sparse weight matrix determines the connections. The random connections are typically shosen from a porbability distribution with a mean of zero and a small variance. This creates a dynamical system that can be used for time-series prediction tasks.
18. Consider the following Continuous time NARX model, result of a training process involving a sum of basis functions $$\ddot{y} = -\frac{1}{3}y^3 - \dot{y} + cos(y)\dot{u} + u$$ where $y, u$ are both real scalars.
	1. State: $[y, \dot{y}, u]$. input: $\dot{u}$
		1. The time evolution of $u$ and $\dot{u}$ cannot be independently selected. $u(t)$ is univocally defined by its initial condition $u(0)$ and the evoution of $\dot{u}$, making the former a state and the latter an input. There is a difference between the input of the original system that you are learning, and the input of the learned model.
	2. Equilibrium
		1. $\frac{d}{dt}(\bar{y}, \dot{\bar{y}}, \bar{u}) = 0 \rightarrow \bar{u} = \frac{1}{3}\bar{y}^3$
		   Only compatible if $\dot{\bar{u}} = 0$
	3. The feedforward part is null for all $\bar{y}$, since input has to be zero.
	   For the linear feedback necessary to generate a locally asymptotically stable closed loop, perform a local analysis via linearization and pole placement.
	   The linearized system can be computed by computing the gradient w.r.t. the state tand of the input and evaluating its value at the desired equilibrium.
19. ![[Pasted image 20240414154223.png]] Option (b) is the most correct as it is based on temporal unrolling and takes care that the prediction capabilites of the model NN extend to the complete prediction horizon of the MPC. Option (a) is also correct since it is the vanilla loss to train a forward dynamic model.
# Week 4
1. How to learn the inverse model of a plant $x_{k+1} = f(x_k, u_k)$, assuming $x$ can be measured and $u$ can be generated by performing experiemnts?
	- Collect dataset on measurable data $x$ and the inputs $u$ that produce these data. Then, train a model to predict control inputs $u$ on $x_k$ that produces output $x_{k+1}$. The error would be the difference between predicted control input value and the actual control input value.
	- Train a model to associate the inputs $(x_k, x_{k+1})$ to the output $u_k$
2. Controller: $u = c(x, \bar{x}, t)$, which keeps the temperature close to the ideal value $y ~= \bar{y}$. $u$ is the degree at which the valve is open at time $t$
	- Use Echo State Network as the machine learning architecture. It has a reservoir of dynamics that has time awareness. So, training this model with data on the ideal temperature the plant should be at through out the day will allow the controller to adapt to disturbances that occur at 2PM.
3. Advantage and disadvantage of deadbeat learning rule
	- Tries to drive the error to zero as quickly as possible.
	- Heavily replies on the prior provided by the linear system, and as a result it is extremely fast to converge.
	- However, relying so much on this prior will lead deadbeat learning rules to suffer robustness issues, as it cannot generalize well and could  overfit.
	- On the other hand, P-rule converges slow because it does not take into account time couplings but it is very robust and can even work without any knowledge of the system's dynamics.
4. 