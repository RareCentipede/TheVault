# Two methods of modeling
## First principle
- Can only deal with parameter uncertainty
- Unrobust to unmodeled phenomena
- Require domain-specific expert knowledge
- Low variance, high bias

## Data-driven modeling
- Deceptive results
- Require access to big data
- Not interpretable
- High variance, low bias

# [[Lagrangian systems]]
- A class of dynamical systems enjoying good properties and characterized by a perculiar methematical structure.![[Pasted image 20240415114413.png]]

# Lagrangian Neural Networks (LNN)
- If it is already known that the system is Lagrangian, then avoid re-learning the Lagrangian structure and learn the various terms in the Lagrangian and in Q, rather than learning $f$ directly.
- The learned dynamics admits application of model-based controllers that leverage the properties of the Lagrangian structure![[Pasted image 20240415114704.png]]