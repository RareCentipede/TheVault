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