# Definition
- Learning succinct and interpretable mathematical expression directly from data
- Learn the best-fitting mathematical model for a dataset, without assuming a specific model structure in advance.

# Sum of Basis Functions
$$y = \sum^{n_p}_{i=1} \pi_i \phi_i (x)$$where $\phi_i(x)$ is the library of symbols $$\mathcal{L} = ||Y - X\pi||^2_2$$
Already a simplly SR algorithm.
- Use generic functions within a library instead of activation functions in a NN-like structure.
- Train as if it was an NN

# Symbolic Regression Through Evolution
- Binary expression tree
	- Represent a mathematical expression
- Nodes are unary or binary operators and leaves are variables or constants
- Represent a generic  mathematical expression as an individual in an EA context
- **Mutation**
	- Change an operator or a leaf
- **Crossover**
	- Swapping parts of two expressions

## SINDy
- Phase 1: learning $$y = \sum^{n_p}_{i=1} \pi_i \phi_i (x)$$$$\mathcal{L} = ||Y - X\pi||^2_2 + ||\pi||_1$$
- Phase 2: Sparsification