- Learn the model/controller while controlling $$\dot{x} = \overbrace{Ax + B(u}^{\text{Linear dynamics}} + \overbrace{\phi^T(x)\pi}^{\text{Sum of basis functions}}$$ assume:
	- $A, B, x$ are known

# Steps
- Pre-learn the model $$\hat{\pi} = X^+ Y$$ where $$X = B\phi^T(x_i)$$$$Y = \dot{x} - Ax_i - Bu_i$$
- Control the system $$u = Kx - \phi^T(x) \hat{\pi}$$
- Update $$\dot{\hat{\pi}} = \phi(x)B^Tx$$