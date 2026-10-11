# Motivation
- Supervised learning -> better predictions -> better control
- Learn non-linear functions
- Estimate the uncertainties of the model
# Gaussian Process Regression
- A generalization of a Gaussian distribution over functions, where any finite number of points from the function's domain follows a multivariate Gaussian distribution.
- To find this distribution in a fully Bayesian way, then a prior distribution over all the possible functions must be defined.
- [[Aleatoric and Epistemic uncertainty]]

## Prior
- Typically specified as a mean function and a covariance function
- Represents our beliefs about the functions before observing any data
	- That our function is a sample of a Gaussian Process defined by a mean function and a kernel matrix $$f(x) \sim \mathcal{GP}(m(x), k(x, x^\prime))$$ where $k(x, x^\prime)$ is the kernel function and $m(x)$ is the mean function.
	- Discrete case $$f \sim \mathcal{N}(m, \Sigma)$$ - The vector $f$ is a sample of a multivariate Gaussian distribution with mean $m$ and covariance matrix $\Sigma$
- For a prior Guassian distribution, the mean vector and covariance matrix must be defined
- For a prior Guassian process, the mean function and the kernel function must be defined.
	- Used to build the covariance matrix later on
- Gaussian distributions that have a covariance matrix with non-zero extra diagonal terms means the different values are correlated, resulting in smooth samples.
	- If the covariance matrix has only diagonal non-zero entries then all values are independent and you just sample noise
- Kernel functions give the correlation between the discretized points

## Gaussian likelihood
- To make predictions, a likelihood function is needed
	- Captures the probability of observing the data given the function values at speficif points
- The likelihood function in exact GP is assumed to be Gaussian$$y=f(x) + \epsilon \quad \epsilon \sim \mathcal{N}(0, \sigma^2_n)$$ $$p(y|f, X) \sim \mathcal{N}(f(X), \sigma^2_n I)$$

## Posterior
- Combines the prior and the likelihood.
- Capturesr the probability of observing the data given the function values at specific points, according to $$\overbrace{p(f|y, X)}^{\text{posterior}} = \frac{\overbrace{p(y|f, X)}^{\text{likelihood}} \overbrace{p(f|X)}^{\text{prior}}}{\underbrace{p(y|X)}_{\text{marginal likelihood}}} \mathcal{N}(\mu_f, \Sigma_f)$$
- If the prior and the likelihood are gaussian distributed, then the posterior is alos going to be gaussian distributed.
	- If the poterior is in the same probability distribution family as the prior, then they are conjugate distributions, and the prior is a conjugate prior for the likelihood function.
- The data induce a posterior GP which is specified by a posterior mean function and a posterior covariance function.
- To compute the distribution that described the sampled data $y$, solve the integral $$p(y|X, y) = \int{p(y|X, f) p(f|X, y) df = \mathcal{N}(\mu_y, \Sigma_y)}$$ $$\mu = K(X, X)(K(X, X) + \sigma^2_n I)^{-1}y$$ $$\Sigma = K(X, X) + \sigma^2_n - K(X, X)(K + \sigma^2_n I)^{-1} K(X, X)$$
![[Pasted image 20240403151440.png]]
## Prediction
- Given the calculation of the poterior distribution, the prediction of new output values can be computed as $$p(f_*|y, X) = \int{p(f_*|f) p(f|y, X) df}$$ marginalizing over the posterior distribution of the function, given the prior model.
- Given that all the terms in the integral are Gaussian, the integral itself is also Gaussian.
- To make predictions, the mean and the variance of the posterior distribution can be computed as the conditional mean and variance of the multivariate Gaussian distribution, according to  $$\mu_{f_*} = K(X_*, X)(K(X, X) + \sigma^2_n I)^{-1}y$$  $$\Sigma_{f_*} = K(X_*, X) + \sigma^2_n - K(X_*, X)(K + \sigma^2_n I)^{-1} K(X, X_*)$$ where $X_*$ are the prediction inputs and $X$ and $y$ are the training input and outputs and $K$ are the correlations computed using a kernel function.
![[Pasted image 20240403151450.png]]
- Prediction of Gaussian Process posterior and posterior plus likelihood noise
	- The average converges to the zero mean prior when far away from the data
	- Epistemic uncertainty addes up to the aleatoric uncertainty (due to sensor noise)

## Sampling
- The Cholesky decomposition of the covariance matrix is calculated to sampled from a multivariate Guassian Porcess $$LL^T = \Sigma$$ where $L$ is a lower triangular matrix. $$y_{sampled} = Lz + \mu \quad z \sim \mathcal{N}(0, I).$$

# Linear Regression
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

# Aleatoric
- Also stochastic uncertainty
- Representative of unknowns that differ each time the same experiment is run.
- Irreducible

# Epistemic
- Also systematic uncertainty
- Derived from things people could in principle know but does not in practice
- Reducible

# Kernel design
# Kernel definition
- Specifies the covariance between the function values at two points in the input space.
- Assumption
	- Function values that belong to points that are close together in the input space are more likely to be similar
- Measure of similarity between two points in the input space.

## Squared Exponential Kernel
- Infinitely differentiable, defined as $$k_{SE}(x_i, x_j) = \sigma^2_v \exp{(-\frac{1}{2}(\frac{(x_i-x_j)^2}{l^2}))}$$ where $\sigma^2_v$ and $l_d$ are the vertical/output lengthscale and the horizontal lengthscale, respectively.
	- They are hyperparameters of the kernel function and are optimized during the training phase.

### Matern Kernel is the generalized SE kernel
- Additional $\mathcal{V}$ parameter which controls the smoothness of the resulting function
	- Larger -> smoother the approximated function
	- As $\mathcal{V}$ approaches infinity, the kernel becomes equivalent to the SE kernel.

## Periodic Kernel
- Allows one to model periodic functions $$k_{periodic}(x_i, x_j) = \exp{(-\frac{2\sin^2{(\pi(x_i-x_j)^2)/p}}{l^2})}$$ where $p$ is the period and $l$ is the lengthscale function, the same in SE.

## Linear Kernel
- When the relationship between the input and output variables is believed to be linear, defined as $$k_{lin}(x_i, x_j) = \sigma^2_0 + x_i \space \cdot \space x_j$$

## Kernel composition
- Sum and multiply kernels to create a more complex prior distribution that would generalize better outside the known dataset.

## Deep Kernel Learning
$$k_{periodic}(x_i, x_j) = \exp{(-\frac{2\sin^2{(\pi(\psi(x_i)-\psi(x_j))^2)/p}}{l^2})}$$
where $\psi$ can be any non-linear regressor and can be trained with any of the parameters of the kernel.
- Using a generic non-linear function to project the input to a latent manifold keeps the kernel to be well defined.

# Kernel parameters optimization
- The kernel hypterparameters determines the fitting behavior of the GP.
- Try to find the parameters that would maximize the probability of sampling the data from the prior distribution.

# Marginal Likelihood Maximization
- The integral along all the possible output functions sampled from the prior distribution, defined as $$p(y|X) = \int{p(y|f, X) p(f|X) df}$$ which is the marginalization of the likelihood of the data over the whole function value space.
- Also the evidence of the data given in the model.
- The likelihood of sampling the data from the prior distribution.
- Allows to find the set of hyperparameters that would best fit the data.
- Given the exponential nature of the Gaussian distribution, the natural logarithm of the marginal likelihood can be obtained as $$\log(p(y|X)) = \underbrace{-\frac{1}{2}(y^TK^{-1}_yy)}_{\text{data fit cost}} \quad- \underbrace{\frac{1}{2} \log{|K_y|}}_{\text{complexity term cost}} - \quad\frac{n}{2} \log(2\pi)$$ where $K_y = K(X, X) + \sigma^2_n I$ and $n$ is the number of data points.
	- The optimal hyperparameters for the kernel is obtained by the maximization of the marginal log-likelihood.
- Tends to favor the least complex model able to explain the data.
	- Tries to maximize the horizontal lengthscale without making the model too rigid.

# Automatic Relevance Determination
- Scale the input values differently in each dimension..
- The SE kernel with ARD is defined as $$k_{SE}(x_i, x_j) = \sigma^2_v \exp{(-\frac{1}{2}\sum^{D}_{d=1}(\frac{(x_{i, d}-x_{j, d})^2}{l^2}))}$$ as seen in [[Kernel Design]], where $D$ is the number of features of the inputs.
- When the kernel has a different lengthscale for each of the input features, and marginal likelihood maximization is used to optimize the kernel, the optimization process automatically determines the relevance of features in a model, deciding which features are important for predicting the output variable and which can be safely ignored.
- Always tries to find the least complex model.
- ARD is active when a kernel has different lengthscales in different features.

# Active and Interactive learning
# Active Learning with Gaussian Process Regression
- Spacial case of [[Incremental Learning]]
	- The learning algorithm can interactively query a human user or some other information source, to label new data points with the desired outputs.
- Make predictions on many points in the workspace, and only label the locations where the predictions are the most uncertain.
	- Also the principle behind how [[Bayesian Optimization]] works.

## Incremental aggregation of datapoints (post-MLL maximization)
- If there is enough data to infer the hyperparameters of the kernel, then only the update of the covariance matrix has to be performed when aggregating more data to the model. The hyperparameters are kept fixed.
- A least square update can be performed to avoid recomputing the inverse of the covariance matrix.
- The smart update of the (inverse of the) covariance matrix allows to aggregate data to make a confident prediction the next that point is visited.
	- This can be skipped if the uncertainty of the prediction is already small enough.

# Sparse Gaussian Processes
With more data, the computation cost to compute the inverse of the covariance matrix becomes prohibitive.

# Sparse Gaussian Process
- Make the optimization and the prediction calculation of a Gaussian Process faster without losing accuracy.
- Add some extra (latent) variables $\bf{u}$  at a certain input location $Z$ , these are inducing variables, as $f$ and $f_*$  can only communicate through $u$. 
	- $p(f, f_*, u)$ is still Gaussian distributed.
	- $u$ induces the dependencies between trainign and test cases.
- This extra variable could always  be marginalized out given the (consistency) property of a Gaussian Process.
- Approximate the joint prior by assuming that $f_*$ and $f$ are conditionally independent given $u$ (fundamental approximation).

## Making prediction with the sparse model
- Use the Woodbury matrix identity and the sparse nature of the approximated covariance matrix, the computation of a large inverse matrix can be avoided.

## Training the kernel parameters and inducing points location
- Optimize inducing point locations by treating them as a parameter of the kernel.
	- Maximize the marginal likelihood with respect to $Z$
	- Find the best parameters for the prior distribution, including the inducing points' locations.
	- May lead to overfitting in practice

## Stochastic Variational Gaussian Process
- A more computationally scalable bound can be achieved by keeping the additional variation distribution

## Variational Distribution Fitting
- A novel lower bound to the true marginal log-likelihood
	- To fit the variational distribution by maximizing the likelihood of fitting the data given as label
- Can be written as a sum of terms, making it more scalable
	- Still need to compute the inverse of the covariance evaluated on the inducing points
	- Only scales with the amount of inducing points, not the data
- Able to maximize the (lower bound of the) marginal log-likelihood of the data without having to use the whole set of labels at every iteration.

## Predicting with Stochastic Variational Gaussian Process
- Intractable integral, can compute the mean and variance of a test point.
- The prediction will not be affected directly by the dimension of the train set, but only by the mean and variance of the approximated distribution.

# MIMO
# MIMO Gaussian Process
- When dealing with multiple outputs, each one can be modeled as an independent Gaussian Process with different kernel functions and hyperparameters.
	- Fir a Gaussain Process model for each output.
	- Very computationally and memory inefficient.
- Share kernel functions when different outputs can be considered as asmpled from the same generative process.

## Sharing horizontal lengthscales
- Given that the smoothness of the motion can be independent o the cartesian direction, in the case of modeling velocity.

## Sharing output lengthscales
- Must be careful
- Outputs might have different units or different level of energy, so it would not make sense to share their lengthscales.

## Sharing likelihood noise
- Cannot be done if the noise level of the sensors differ a lot.
	- Would make the uncertainty to be miss-calibrated.
- When going into unexplored regions of the workspace, having well-calibrated uncertainty can make a huge difference between a usable and unusable uncertainty prediction.

## Sharing the inducing inputs
- Having different inducing inputs for each output can be intractable when fitting a sparse model.
- Sharing the inducing points among the different outputs can speed up the fitting process and does not have many disadvantages.