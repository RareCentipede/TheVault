# Non-linear Dynamics and Control, Learning the model
## Continuous-Time Non-linear Affined State-Space model 
![[Pasted image 20240416111811.png]]

## To obtain the model
1. Physical modeling
	- First principles -> differential equations
2. Data-driven: System Identification/Machine Learning
	- Measure input-output data
	- Postulate model structure (linear-nonlinear)
	- Estimate model parameters from data (least square)

## Lyapunov stability
![[Pasted image 20240416113018.png]]

## Continuous-Time Linear Systems
- A dynamical system is linear is $f(x) + g(x)u$ and $h(x, u)$ are linear simultaneously w.r.t. $x$ and $u$. ![[Pasted image 20240416113221.png]]

## Discrete-Time Linear Systems
![[Pasted image 20240416113334.png]]

## Equations of motion
**Fully actuated mechanical system**
- $M(q)\ddot{q} + C(q, \dot{q})\dot{q} + G(q) + D(q)\dot{q} = \tau$
**PD + Gravity compensation**
- $\tau = K_p(\hat{q} - q) + K_d(\hat{\dot{q}} - \dot{q}) + G(q)$
**PD + Feedforward**
- $\tau = K_p(\bar{q}-q) + K_d(\dot{\bar{q}}-\bar{q}) + M(\bar{q})\ddot{\bar{q}}) + C(\bar{q}, \dot{\bar{q}})\dot{\bar{q}} + G(\bar{q}) + D(\bar{q})\dot{\bar{q}}$
- From linearizing the system around the desired trajectory
- Can also be analyzed theoretically in the fully non-linear setting, showing that the tracking error will be bounded if the desired trajectory is slow enough and the control gains are high enough.
**PD+**
- Similar to PD+FF but all the terms are calculated using the current $q$ and its derivative, rather than the reference.
- Can achieve imporved performance and provable steady state null error
- However, C needs to be calculated with Christoffel symbols which is inefficient
**Computed Torque (FB-Linearization MIMO)**
- Everything evaluated in the current configuration and velocity
	- Acceleration not part of the state
- Strongly improved performance in the nominal case
- The only controller ensuring exponential convergence
- Requires very good knowledge of the model

# Artificial Neural Networks, Deep Learning, Model Learning
## Sum of basis functions
![[Pasted image 20240416120155.png]]

## Activation functions
![[Pasted image 20240416120447.png]]

## Feedforward neural network
![[Pasted image 20240416120616.png]]

## Approximation properties of neural nets
- $$J = \mathcal{O}(\frac{1}{h})$$
- $$J = \mathcal{O}(\frac{1}{h^{2/P}})$$

## Convolutional Neural Networks
To process grid-like information like images.

### Weight sharing: spatial equivariance
- Share pieces of network
- Copy the part of the network across the input space, enforce that the weights remain equal.

### Convolution
- Instead of copying parts of the network, slide a part of the network over the input
- Convolution: $$S(i, j) = (I * K)(i, j) = \Sigma_m \Sigma_n I(m, n)K(i - m, j - n)$$
- Detect non-linearities on top of the feature map.
- Optional pooling: take some function over the area of the kernel.

# Advanced ANNs
## Time-aware architectures
### Temporal unrolling
- An alternative to vanilla regression loss when learning dynamical systems
	- Especiall in continuous time
- Train a neural network to approximate the behavior of a non-linear dynamical system. Assume that the state can be measured.
- Time evolution of the learning dynamics $$\bar{x}(t) + \int^T_0NN_w$$
### Learning the model from outputs
- Input is hidden by the output function.
- Reasons:
	- Natural representation of the state is clear, but there is no collocated sensors
	- No idea about the nature of the underlying state of the system
- Learn the dynamics of systems when it is not possible to directly measure or even characterize the state
- A non-linear time-discrete system: $$x_{k+1} = f(x_k, u_k), \quad y_k = h(x_k)$$
	- When $y_k$ is an admissible state representation of the system, meaning it carries all the neccessary information on the system behavior, it can be used as a system state and directly learn $f_y$ in $$y_{k+1} = f_y(y_k, u_k)$$

### Delayed outputs
- $h$ might not always be invertible, since the state $x$ could contain both the configurations of the system and the associated time derivatives, and only the former can usually be measured.
	- Hence, $h: \mathbb{R}^{2n} \rightarrow \mathbb{R}^n$ and cannot be inverted $(2n < n$).
- Add delayed outputs

## Recurrent Neural Networks
#### Concept
- Neural Networks including neurons with internal dynamics (recurrent units/neurons)
- Difficult to learn long term dependencies due to the exploding/vanishing gradient problem
#### Training (Back Propagation Through Time (BPTT))
- Make $n$ copies of the network, calculate $[y_1, \dots , y_n]$
- Start at time step $n$ and propagate the loss backwards through the unrolleld networks
- Update the weights based on the average gradient of the network copies

## Echo States Network
#### Reservoir computing
- A complex dynamical system that is excited through the input layer. in ESNs, the reservoir is implemented as a randomly connected neural network.
- During trianing only the output layer weights $w_{out}$ are adapted. Input layer and reservoir remain fixed.

#### Echo State Network (ESN)
- Linear in the parameteres, which means closed form training when using L2 norm.
- The training set must contain examples that excite all the relevant dynamic response of the reservoir.
- The reservoir's weights $w$ must be extracted from a distribution that assure simultaneously dynamic richness (edge of chaos) and asymptotic stability.![[Pasted image 20240414144141.png]]

## Lagrangian Neural Networks
### Two methods of modeling
#### First principle
- Can only deal with parameter uncertainty
- Unrobust to unmodeled phenomena
- Require domain-specific expert knowledge
- Low variance, high bias

#### Data-driven modeling
- Deceptive results
- Require access to big data
- Not interpretable
- High variance, low bias

## [[Lagrangian systems]]
- A class of dynamical systems enjoying good properties and characterized by a perculiar methematical structure.![[Pasted image 20240415114413.png]]

## Lagrangian Neural Networks (LNN)
- If it is already known that the system is Lagrangian, then avoid re-learning the Lagrangian structure and learn the various terms in the Lagrangian and in Q, rather than learning $f$ directly.
- The learned dynamics admits application of model-based controllers that leverage the properties of the Lagrangian structure![[Pasted image 20240415114704.png]]

## S(pike) NN
- The A particular type of ANN in which the function of the neurons and the synapses in the network are more _inspired by biology_ than other types of ANNs![[Pasted image 20240415115343.png]]

### Neuron dynamics
- Static in ANNs
- SNNs can employ various biologically simulated neuron dynamics
- Leaky Integrate-and-Fire model is the most popular

## Firing mechanism and reset machanisms
- The output is the results of the firing mechanism
- After firing a spike, membrane potential is the result of the reset mechanism

## Advantages
### Energy efficiency
- Event-based calculation
- Data stream is binary, so multiplication becomes addition
- Edge computing applications

### Temporal information processing
- Richer neuron dynamics compared with static neural networks.
- Useful in event-based scenarios
	- High temporal resolution
	- Event-based sensors

# Direct Control Learning, Imitation Learning, Iterative Learning Control
![[Pasted image 20240415122205.png]]
## Learn a controller directly to drive the error signal to zero or to maximize/minimize some reward/cost

### Option 1: direct learning of the inverse model
- Learn $f^{-1}$ such that $f(x^d_k, f^{-1}(x^d_k, x^d_{k+1})) = x^d_{k+1}$ ![[Pasted image 20240415122600.png]]
- Can be made into a feedforward action by generating the current state/output as delayed reference or through a pre-learned forward model ![[Pasted image 20240415122909.png]]

### Option 2: imitation learning
- When examples of an ideal controller (teacher) is available, regression strategies can be used to copy the teacher ![[Pasted image 20240415123045.png]]
- Can be expert human operators, or computationally expensive controller
- The training can be both online and offline
	- **Online:** the teacher can be interrogated to get new examples
	- **Offline:** the dataset is pre-collected and cannot be changed
- 