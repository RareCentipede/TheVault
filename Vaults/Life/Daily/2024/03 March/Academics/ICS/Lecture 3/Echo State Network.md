# Reservoir computing
- A complex dynamical system that is excited through the input layer. in ESNs, the reservoir is implemented as a randomly connected neural network.
- During trianing only the output layer weights $w_{out}$ are adapted. Input layer and reservoir remain fixed.

# Echo State Network (ESN)
- Linear in the parameteres, which means closed form training when using L2 norm.
- The training set must contain examples that excite all the relevant dynamic response of the reservoir.
- The reservoir's weights $w$ must be extracted from a distribution that assure simultaneously dynamic richness (edge of chaos) and asymptotic stability.![[Pasted image 20240414144141.png]]