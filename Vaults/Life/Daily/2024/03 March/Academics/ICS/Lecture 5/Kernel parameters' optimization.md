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