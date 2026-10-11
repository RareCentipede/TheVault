#todo 
Q1 Week 5
## Lauren
- 2nd drone issues fixed
- Test flight when weather is good
- Start on ROS2 integration
- All for x500
- Test flight with the Avular drone for data aquisition
- Monitor RTK fix situation

## Shawn
- Get some mapping
	- Work on localization with LiDARs
	- ICP
- 3 Sources of input
	- PX4 sitl gazebo
	- Airsim sensor input
		- No noise, need filter
	- From actual drone
- Compare all these results

## Zhengyang
- Tom, Lauren and I are preparing for Wednesday's TU/e meeting (1PM)
- Mission Director
	- Code integration in collaboration with Tom
	- Simulate code
	- Potentially test drones with generated sample way-points
- Create more representative conditions in AirSim, such as artificial noise
## Tom
- Make dummy node to represent the perception part, so the whole system can be integrated smoothly
	- Interface with visual modules
- Make discussion notes for Wednesday
- Figure out how to deal with edge cases
- Make difficult waypoints to test the system

## Abir
- Sent segmentation results to Mani
- Meet with Mani for feedback
	- Might be overfitted
- Try out bird-eye view idea

## Akhilesh
- Will give updates next Friday

## Mani
- Acquire data from the drones
- Provide Shawn with data to work with
- Plan meeting with Ali and maybe also Shawn
	- Discuss the use of LiDAR to obtain point-cloud data
- Plan meeting with Abir and Ali for drone traversal birds' eye view
	- In-person on Thursday afternoon

## Stefaan
- Moving back to Delft
- Plan meeting with Niels
- Deriving and choosing internal milestones

## Action points
- Plan meeting between Mani and Ali (maybe also Shawn) to discuss use LiDAR to obtain point-cloud data
- Study justification of using LiDAR to get point-cloud data rather than RGB-D or other options
- Mani plans meeting with Abir and Ali for drone traversal birds' eye view
	- In-person on Thursday afternoon
	- Mani make agenda 
- Mani sends Ali the github repo for point-cloud registration