# Articial neuron
![[Pasted image 20240327163056.png]]
- $x_i: i^{th}$ input of the neuron
- $w_i:$ adaptive weight (synaptic strength) of $x_i$
- $z:$ weighted sum of inputs: $z = \sum^p_{i=1} w_i x_i = \bf{w^T x}$ 
- $\sigma(z):$ activation function
- $v:$ output of the neuron

# Activation function
- Purpose: transformation of the input space (squeezing)
- **Projection functions**:
	- Threshold function, piece-wise linear function, tangent hyperbolic, sigmoidal, rectified linear etc
- **Kernel functions**:
	- Radial basis function

# Gradient descent
- Train a neuron to minimize the error of the output using the weights

# Backpropagation
- Initialize network weights with small random values
- Repeat until the performance on a separate test-set stops improving:
	- **Forward pass:** Given an input x, calculate the neural network output $y=f(x, W)$, then calculate the cost $J(y, t)$ of predicting $y$ instead of target output $t$
	- **Backward pass:** Calculate the gradient of the cost with respect to the weights $\Delta J(y(x, W), t) = [\frac{\partial J}{\partial w_1}, \dots, \frac{\partial{J}}{\partial{w_n}}]^T$ 
	- **Optimize:** Update the weights based on the gradient to reduce the cost.

# Cost functions
## Types
- Classification
- Regression
- Regularization
## Two main criteria
- The minimum of the cost function should correspond to the desirable behavior
- The error gradient should be informative

# Optimizers
## [[Stochastic Gradient Descent]]
- Randomly picks one data point from the dataset at each iteration for gradient descent.

## [[Momentum]]
- Increase step-size if we keep going in the same direction

## [[RMSProp]]
- Decrease step-size over time, especially if gradients are large

## [[ADAM]]
- Combine Momentum and RMSProp and correct for their initial bias

# [[Architectures]]