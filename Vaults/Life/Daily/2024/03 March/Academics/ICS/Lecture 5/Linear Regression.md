# Ordinary Linear Regression
- Statistical model which estimate the linear relationship between a scalar response and one or more explanatory variables (dependent and independent variables).
	- $y = f(x) = x \bf{w}$
	- Least squared solution of the parameters:
		- $w = (X^T X)^{-1} X^T y$

# Kernelized Linear Regression
- A technique that applies the kernel trick to linear regression.
- Transforms the input features into a higher-dimensional space $\phi$, where they are linear to capture non-linear relationships.
- Regression is then performed in this transformed space, effectively modelling non-linear patterns in the data while still using a linear model.
	- Computationally expensive for large datasets due to the need to compute pairwise kernel evaluations.
- Mathematically,
	- $y = f(\phi(x)) = \phi(x) w$
		- $\phi(x) \in \mathbb{R}^{N\times L}$ 
		- $y \in \mathbb{R}^{N \times o}$
		- $w \in \mathbb{R}^{L \times o}$
		- $L:$ the number of newly projected features
		- $o:$ the number of output features
		- $N:$ number of observations
- If the number of extracted features is very big, the calculations of the matrix $\bf{w}$$$\bf{w} = (\phi(\bf{X})^T \phi(\bf{X}))^{-1} \phi(\bf{X})^T \bf{y} $$ will be intractable given the inversion of the matrix.
	- However, given that there are $N$ data points, the solution of the parameteres must be correlated between them and the maximum $N$ parameters can be independent.
- Hence, $w$ can be written as a linear combination of data points $$\bf{w} = \phi(\bf{X})^T \bf{\alpha}$$
	where $\alpha \in \mathbb{R}^{N \times o}$.
- Define $\bf{K} = \phi(\bf{X}) \phi(\bf{X})^T$ then $$\bf{\alpha} = \bf{K}^{-1} \bf{y}$$
- Hence, to make prediction on a new point $$f(x_*) = \phi(x_*) \phi(\bf{X})^T \bf{K}^{-1} \bf{y}$$
## Kernel trick
- Allows algorithms to implicitly operate in a higher-dimensional space by computing the dot product between data points in this space without actually having to compute the transformation of the data points into the higher-dimensional space.
- Difficult to find the kernel function that corresponds to a particular $\phi$ vector.
- Dot product is an operator of similarity between vectors, the kernel between two inputs can be seen as how similar the projected vectors would be in these other spaces.

## Bayesian Linear Regression
- A statistical approach to linear regression that incorporates Bayesian principles.
- Provides a probability distribution over possible values of the coefficients.
	- Updated based on prior beliefs about the coefficients and observed data, allowing for uncertainty to be quantified. 
	- Mathematicall, $$f(x)=xw$$or$$p(f|x, w) = \mathcal{N}(xw, 0)$$
- Assume that the observation of the data is the true function plus a Gaussian noise
	- $y = f(x) + \epsilon$ 
	- $\epsilon \sim \mathcal{N}(0, \sigma^2_n)$
- Hence, the likelihood of observing the data is also gaussian distributed with linear mean and a diagonal covariance matrix
	- $p(y|X, w) = \mathcal{N}(Xw, \sigma^2_n I)$
- To find the probability distribution of the parameters, start from a prior distribution and use [[Bayes theorem]] to make predictions, then marginalize.