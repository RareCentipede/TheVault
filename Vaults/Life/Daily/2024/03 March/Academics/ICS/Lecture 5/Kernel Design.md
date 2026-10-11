# Kernel definition
- Specifies the covariance between the function values at two points in the input space.
- Assumption
	- Function values that belong to points that are close together in the input space are more likely to be similar
- Measure of similarity between two points in the input space.

## Squared Exponential Kernel
- Infinitely differentiable, defined as $$k_{SE}(x_i, x_j) = \sigma^2_v \exp{(-\frac{1}{2}(\frac{(x_i-x_j)^2}{l^2}))}$$ where $\sigma^2_v} and $l_d$ are the vertical/output lengthscale and the horizontal lengthscale, respectively.
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