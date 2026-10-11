# Parametric models
- A learning model that summarizes data with a set of parameters of fixed size (independent of the number of trainign examples).
- No matter how much data you throw at a parametric model, it won't change its mind about how many parameters it needs.
- Parametric approximator + Learning strategy

## Parametric approximators
- $y = M(x; \pi)$
	- $y:$ output
	- $M:$ approximator model
	- $x:$ input
	- $\pi:$ parameters

## Parametric regression
- Given a dataset of points, find the set of parameters that best explain these data w.r.t a given similarity measure