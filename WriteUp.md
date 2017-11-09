# CarND-Path-Planning-Project
Self-Driving Car Engineer Nanodegree Program
  
### Writeup
The objective of this project was to design a vehicle path planner that would interact with the provided Udacity simulator, to provide a path as a set of waypoints back to the simulator. This path planner had to take perfect map and sensor fusion data into account and generate a path that was collision free, obeyed the speed limit, and ensured acceleration and jerk were within allowable limits. The vehicle was also expected to change lanes when necessary in order to pass slower vehicles. I will describe how I was able to accomplish this by addressing each rubric points below.

1. The car is able to drive at least 4.32 miles without incident..
This is made possible by addressing each of the other rubric points, so I will discuss each of those separately.

2. The car drives according to the speed limit.
This was done by following the technique used in the project walkthrough video. A maximum reference velocity is set to 49.5 mph. The desired reference value is then used to space the path waypoints in order to ensure the speed limit is not exceeded.

3. Max Acceleration and Jerk are not Exceeded.
This is done also by following the techniques used in the project walkthrough video. First, the longitudinal acceleration is limited by limiting the change in reference velocity each timestep. The lateral acceleration and jerk are considered by how the waypoints are generated. First, several waypoints are placed sparsely apart, according to the desired lane, 30m apart. Then, a spline used to smoothly connect the current vehicle position to those sparsely placed waypoints. This helps keep jerk and acceleration in the acceptable limits. 

4. Car does not have collisions.
This is accomplished by using the sensor fusion data reported by the simulator, which reports the location and speed of other vehicles on the road. This is done in lines 260-315. Each vehicle reported by the simulator is checked. First, the lane of the vehicle is determined and compared to our vehicle's lane. If the vehicle is in our lane, I check its location (in Frenet Coordinates) and speed. If it is close in front of us, flags are set to indicate our desire to change lanes if possible, and also to start to slow down to follow the vehicle in front of us. If the vehicle is in one of the adjacent lanes, I determine its relative longitudinal position on the road, and its speed and determine if it is preventing us from changing lanes. These checks ensure that I will not plan a path into another vehicle on the road.

5. The car stays in its lane, except for the time between changing lanes.
Frenet coordinates are used to set the desired location of the vehicle in the lane. This makes it easy to make sure the vehicle stays in the desired lane until there is a desire to change lanes.

6. The car is able to change lanes
After it is determined that changing lanes is safe, as described in point 4, the desired lane is changed, and that new lane is used to generate the sparsely located waypoints for the new path.



