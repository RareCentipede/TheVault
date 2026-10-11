![[Pasted image 20240415122205.png]]
# Learn a controller directly to drive the error signal to zero or to maximize/minimize some reward/cost

# Option 1: direct learning of the inverse model
- Learn $f^{-1}$ such that $f(x^d_k, f^{-1}(x^d_k, x^d_{k+1})) = x^d_{k+1}$ ![[Pasted image 20240415122600.png]]
- Can be made into a feedforward action by generating the current state/output as delayed reference or through a pre-learned forward model ![[Pasted image 20240415122909.png]]

# Option 2: imitation learning
- When examples of an ideal controller (teacher) is available, regression strategies can be used to copy the teacher ![[Pasted image 20240415123045.png]]
- Can be expert human operators, or computationally expensive controller
- The training can be both online and offline
	- **Online:** the teacher can be interrogated to get new examples
	- **Offline:** the dataset is pre-collected and cannot be changed
- 