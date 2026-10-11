# Concept
- Neural Networks including neurons with internal dynamics (recurrent units/neurons)
- Difficult to learn long term dependencies due to the exploding/vanishing gradient problem
# Training (Back Propagation Through Time (BPTT))
- Make $n$ copies of the network, calculate $[y_1, \dots , y_n]$
- Start at time step $n$ and propagate the loss backwards through the unrolleld networks
- Update the weights based on the average gradient of the network copies