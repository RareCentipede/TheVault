# Ideal end-product
- User teleoperates the robot to build something in the simulation
- The demonstraion is saved then optimized
- The optimized operation for this particular structure can be dispatched to the real robot
	- This is generalized to different surfaces and orientations
- The robot allocates resources in a smart way

# Components
## Teleoperation
- Can be done in simulation to avoid delays
- Basic movements
- Singularity configuration detection
- Grasping

## Learning and Optimization
- Learn from the demonstrations
- Build a reinforcement learning model to optimize the demonstration to repeat it better
	- Since a reference is available, the learning task could be easier
	- Both position of the robot and the manipulator movement
- Output: mobile platform and arm control inputs
	- Moving the platform towards the desired location can be done via classical path planning and control methods
	- The building operation itself could be improved via small movements in the mobile platform
- Demonstrate the optimized motion plan in simulation first. The user should confirm it to update the plan.

## Sim2real
- Dispatch the optimized motion plan onto the real robot
- Rebuild the reference structure at any valid position and orientation

# Research direction
- Imitation learningor reinfocement learning model for optimizing and generalizing demonstrated operations
	- Generalize to different shapes, positions, and orientations of structures
	- Has stacking things been done before?
- Priority of the thesis would be on creating a good framework for imitation and reinforcement learning. Then teleoperation can be added to create references and demonstrations for the robot to follow and trained on. Sim2real should be focused on last for validation.
- There has been extensive work on all these topics, so there is plenty of literature study to do

# Research plan
- Read up on some notable papers on
	- Optimize and generalize learned demonstration using reinforcement learning models or imitation learning
	- Combinatorial control of mobile platform and manipulator
- Check out their limitations and next steps to get inspirations