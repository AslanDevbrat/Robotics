# RROBOTICS FINAL PROJECT

## FOLLOWER APPLICATION
- In this we have two turtle in the Turtlesim
- One turtle is controlled by the teleope_node i.e by the keyboard

- The other Turtle follows it.

https://user-images.githubusercontent.com/39759685/141657039-64d2a51d-3927-45b5-a922-23ef5f326b26.mp4


## CODE STRUCTURE

- TF Broadcaster was created

  - It broadcast the frame of the Turtlesim

- A TF Broadcaster was Assigned to every Turtlesim

- TF Listener was Created

  - It gets the Transformation between the two frames

  - It Extracts the distance and Orientation

  - It make the Turtle2 move Toward the Turtle1 using go to goal Behaviors

## FRAMES DETAILS

- `rosrun tf2_tools view_frames.py`
- <img width="815" alt="Capture" src="https://user-images.githubusercontent.com/39759685/141657186-12471393-629c-44f5-99c2-2a33f1e65021.PNG">


## MAP BASED NAVIGATION
- First I created a Occupancy Grid Map

- Each cell hold a probability of occupancy 0% to 100%

- Areas that are unknown are marked as -1

- White cell means Free space

- Black cell means Obstacle

- Grey cell means Unexplored Area
- <img width="123" alt="occapancy grid" src="https://user-images.githubusercontent.com/39759685/141657203-e2a85bcb-3e29-4bf8-9b29-8af9402ac0bd.PNG">



## VIDEO DEMO OF USING SLAM ALGORITHMS

- `roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping`

- The following video show the mapping



https://user-images.githubusercontent.com/39759685/141657244-14a9ca51-ed01-45a8-80a9-7e51218d1406.mp4




### MAP CREATED
![tb3_house_map](https://user-images.githubusercontent.com/39759685/141657265-e80dff4f-491f-4714-a2da-145869660eb3.png)


## NAVIGATION SUMMARY

- We first need to manually set the initial location of the robot in the map using
2D Pose Estimate.
- We send goal poses (location+orientation) using 2D Nav Goal, so that the
robot moves to it.

  - The navigation stack has two motion planners:

    - Global Path Planner: plans a static obstacle-free path from the location of the robot to the goal location
    - Local Path Planner: execute the planned trajectory and avoids dynamic obstacle.

## FRAMES MAP
<img width="811" alt="fromae_nav" src="https://user-images.githubusercontent.com/39759685/141657476-1be18020-db97-40a6-86d0-20db3b457810.PNG">

## DWA ALGORITHMDWA ALGORITHM

▸ Discretely sample in the robot's control space (dx,dy,dtheta)

▸ For each sampled velocity, perform forward simulation from the robot's current state to
predict what would happen if the sampled velocity were applied for some (short) period
of time.

▸ Evaluate (score) each trajectory resulting from the forward simulation, using a metric
that incorporates characteristics such as: proximity to obstacles, proximity to the goal,
proximity to the global path, and speed. Discard illegal trajectories (those that collide
with obstacles).

▸ Pick the highest-scoring trajectory and send the associated velocity to the mobile base.

▸ Rinse and repeat.<img width="228" alt="dwa" src="https://user-images.githubusercontent.com/39759685/141657500-4d381eac-08a6-4851-99bd-5a15db97d1b6.PNG">


## TRAJECTORY SCORING


<img width="448" alt="trajectory_scoring" src="https://user-images.githubusercontent.com/39759685/141657516-5499f127-756c-478a-b48f-9d2c799c9259.PNG">

- Path_distance_bias helps penalizing trajectory far from global path .

- goal_diatnce_bias penalize trajectories far from goal locations

- Occdist_scale help selecting trajectories far from obstacles.

# PARAMETER TUNING

- In the following video I tune the previously mentioned parameter Dynamically

- The short yellow color line denotes the path given by local path planner

- The longer deep blue line show the path given by the global path planner

- Notice When I set Path_distance_bias to zero the robot travel more in the direction given by local planner.

- When I set goal_diatnce_bias to zero the robot follows the path given by the global planner

- When Occdist_scale is set to high value then the robot start to spin because I think everywhere obstacle is present and in order to avoid them it start to spinning




https://user-images.githubusercontent.com/39759685/141657574-71154fa5-25bd-4b8e-9bea-d3bcfd73e289.mp4

