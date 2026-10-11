# Motivation
- [Modular blocks for lunar infrastructure](https://www.sciencedirect.com/science/article/pii/S0094576523001121)
- [Study on Modular Blocks for Lunar Habitable Infrastructure](https://www.scopus.com/record/display.uri?eid=2-s2.0-85207966038&origin=resultslist&sort=plf-f&cite=2-s2.0-85150061830&src=s&imp=t&sid=d33097ba87d588efe5fd1d949acea313&sot=cite&sdt=a&sl=0&relpos=6&citeCnt=0&searchTerm=)
- [Why Modular Building Hasn't Revolutionized Construction](https://hbr.org/2023/12/why-modular-building-hasnt-revolutionized-construction)
- [Life on Mars](https://parametric-architecture.com/what-could-architecture-possibly-look-like-on-other-planets/?srsltid=AfmBOooAUUtPo9Q0Ddi-KnPDM_q3Wb7YnrthwGP7GQssts6yGJH0g5nN)
- [Modular Construction of Topological Interlocking Blocks—An Algebraic Approach for Resource-Efficient Carbon-Reinforced Concrete Structures](https://www.mdpi.com/2075-5309/13/10/2565)

## Modular building blocks
- EZBlocks
- Everblocks
# HRI through virtual interface
- [HRCod](https://etd.ohiolink.edu/acprod/odb_etd/etd/r/1501/10?clear=10&p10_accession_num=kent1619714568614344)
- Build shelters that cover a user-defined area as much as possible
- Uses one type of components for simplicity
# Reinforcement learning for mobile manipulation
- [Learning Mobile Manipulation through Deep Reinforcement Learning](https://www.mdpi.com/1424-8220/20/3/939)
	- Moves different items
	- Could look into stacking and more complex building
- [Distributed Reinforcement Learning of Targeted Grasping with Active Vision for Mobile Manipulators](https://ieeexplore-ieee-org.tudelft.idm.oclc.org/document/9341605)
	- Grasp unseen objects in a cluttered environment
- [Compact Multi-Object Placement Using Adjacency-Aware Reinforcement Learning](https://ieeexplore-ieee-org.tudelft.idm.oclc.org/document/10769899)
	- Place irregularly shaped objects as closely together as possible
	- Considers spatial constraints with neighbors
	- Places objects in a given layout

# Computer vision module
## Block/object segmentation

## Object identification

## Grasping
[Robot Grasping of Novel Objects](https://www.semanticscholar.org/paper/Robotic-Grasping-of-Novel-Objects-Saxena-Driemeyer/a1466825412cdec8f853edf14d95de4c5edc0510)
- Vision-based
- Supervised learning
- Does not require or builds a 3-d model of the object
- Was able to successfully grasp objects it had never seen before

[Robotic Grasping of Unknown Objects Using Novel Multilevel Convolutional Neural Networks: From Parallel Gripper to Dexterous Hand](https://ieeexplore-ieee-org.tudelft.idm.oclc.org/document/9180002)
[Automatic grasp planning using shape primitives](https://www.semanticscholar.org/paper/Robotic-Grasping-of-Novel-Objects-Saxena-Driemeyer/a1466825412cdec8f853edf14d95de4c5edc0510)
[SuperQ-GRASP](https://rpm-lab-umn.github.io/superq-grasp-webpage/)
[Robotic Objects Detection and Grasping in Clutter Based on Cascaded Deep Convolutional Neural Network](https://ieeexplore-ieee-org.tudelft.idm.oclc.org/document/9627972)

## Collision avoidance using LiDAR

# Building logic
## Order of block placement and pickup

## Knapsack problem

# Block placement
## Stacking
### [Stacking of Diverse Shapes with Large-Scale Iterative Reinforcement Learning on Real Robots](https://ieeexplore.ieee.org/abstract/document/10610297?casa_token=8mMJkRU9JJcAAAAA:JTw3i9ZCQfYFDn1hFNN5enfKwnVvKAUAHrQ_ww1Ja4MdKZ10AlaSg8WkfYWcgXhi5wRBtuU4)
### [Efficient Stacking and Grasping in Unstructured Environments](https://link.springer.com/article/10.1007/s10846-024-02078-3)
- Decomposing long-horizon tasks into smaller sub-tasks
- Hierarchical Reinforcement Learning
- Both stacking AND alignment. Crucial to build a beautiful house :)

### [Grasp for Stacking via Deep Reinforcement Learning](https://ieeexplore-ieee-org.tudelft.idm.oclc.org/abstract/document/9197508?casa_token=lbl2dNi5FKkAAAAA:SFg3bc0z3Lw0ISALF9PGw8GrAKpg6qFoIZJW9FHBRdl7FOzWOsKmd_x10VmLf4Q98Vo0_cAT)
- Two networks
	- Grasping network
		- Predict pixel-wise grasping position
		- Which object is easy to grasp, and which one is needed in the stacking area
	- Stacking network
		- Predict block-wise stacking position
- Auxiliary tasks
	- Predict the number of objects on the desk
	- Heap height prediction
	- Object-centric feature learning task
		- Ensures the object that disappears from the desk is similar to the one that is added to the pile
- Q-learning
	- Distributed prioritized experience replay
		- Learn policies that could grasp different size of boxes and place them tightly on a platform
- Can only make a wall. The gripper cannot operate when the fingers are blocked by other objects

### [Autonomous robotic stone stacking with online next best object target pose planning](https://ieeexplore.ieee.org/abstract/document/7989272?casa_token=71RcOU83wiAAAAAA:jaDYyBSI6iHTvC2iLtvHk_Ui0LzA7O2v4ZKJRUPUTBReQNx8Hhja6tUEU6bpsrpaERrTMPIA)
- System consisting of
	- An object detection pipeline
	- A pose searching algorithm considering structural stability using a physics engine
	- An autonomous system for constructing balancing vertical towers using a manipulator
- Overview:
	- Prescanned models of stones
	- Online scan of stones using RGB-D camera and matching between scanned observed stone and scanned stone
	- Estimate the optimal pose to place the stone
	- Execute the movement using MoveIt!

### [Beyond Pick-and-Place: Tackling Robotic Stacking of Diverse Shapes](https://openreview.net/forum?id=U0Q8CrtBJxJ)
- Pick and place of diverse and dynamic objects
- Vision-based
- Simulation-trained agents, collect data in the real world, which are then used for further performance improvement with offline RL
- Real-world evaluations
- Gap between skill mastery and skill generalization

[Mobile Manipulator for Autonomous Localization, Grasping and Precise Placement of Construction Material in a Semi-structured Environment](https://arxiv.org/abs/2011.07972?utm_source=chatgpt.com)

[Robotic Stacking of Irregular Objects with Load Position Identification and Compensation](https://ieeexplore-ieee-org.tudelft.idm.oclc.org/document/10260654)
- Size recognition, position identification and compensation of load
- Stacking position detection
- Force sensor

[A Reinforcement Learning Method for Rearranging Scattered Irregular Objects Inside a Crate](https://ieeexplore-ieee-org.tudelft.idm.oclc.org/document/9904530)

[PackerBot: Variable-Sized Product Packing with Heuristic Deep Reinforcement Learning](https://ieeexplore-ieee-org.tudelft.idm.oclc.org/document/9635914)


## Adjust mobile platform position for optimal placement


## Some new papers
[Robot that flips a piano](https://app.dimensions.ai/details/publication/pub.1141538014)
[Manipulator with insufficient payload](https://app.dimensions.ai/details/publication/pub.1160241184)
[Rotating objects via in-hand rotating](https://ieeexplore.ieee.org/document/10341505)
[Basics of pick and place](https://manipulation.csail.mit.edu/pick.html)