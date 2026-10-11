# SNN
- The A particular type of ANN in which the function of the neurons and the synapses in the network are more _inspired by biology_ than other types of ANNs![[Pasted image 20240415115343.png]]

# Neuron dynamics
- Static in ANNs
- SNNs can employ various biologically simulated neuron dynamics
- Leaky Integrate-and-Fire model is the most popular

# Firing mechanism and reset machanisms
- The output is the results of the firing mechanism
- After firing a spike, membrane potential is the result of the reset mechanism

# Advantages
## Energy efficiency
- Event-based calculation
- Data stream is binary, so multiplication becomes addition
- Edge computing applications

## Temporal information processing
- Richer neuron dynamics compared with static neural networks.
- Useful in event-based scenarios
	- High temporal resolution
	- Event-based sensors

# Challenges
## Software
- No unified training method
	- Due to the firing mechanism, back propagation in ANNs could not be directly used anymore

## Hardware
- Should be deployed on neuromorphic chips
	- Many work could only use GPU to simulate the neuromorphic chips