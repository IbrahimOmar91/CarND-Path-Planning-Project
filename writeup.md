## Here What i did,
First we have to initialize the car, so i started with 0 speed and lane to the center lane [1]<br>
Then got the sensors data of all the cars to decide what to do.<br>
Foreach car in them i got its data and predict the next position **S** for each one.<br>
For our new path point to be calculated we have to make sure that the path is collision free, within the acceleration and jerk limits.

### This could be done by the following steps:
#### Check for the other car to see its lane and distance from us<br>
`if it is in the same lane and 25 meters or closer to us so we set a flag [carFront] to true.`<br>
`if it is on the right lane and within 30m front and 8m back we set a flag [carOnRight] to true.`<br>
`if it is on the left lane and within 30m front and 8m back we set a flag [carOnLeft] to true.`<br>

#### Based on the flags we decide:
if car in front whatever the lane, we decelerate **reduce speed by 0.4**, then check the lane:<br>
.. if left lane [0] and right lane [2] is free >> change lane to center [1]<br>
.. if center lane [1] then check other two lanes:<br>
.... if left lane [0] is free >> change lane to left [0]<br>
.... if left lane [0] is occupied and right [2] is free >> change lane to right [2] <br>
.. if lane 2 and center lane is free >> change lane to center [1]<br>
if there is not car in front and speed is lower than 49.5 >> accelerate<br>

Then Create a list of widely spaced (x,y) waypoints, evenly spaced at 30m Later we will interpolate these waypoints with a spline and fill it in with more points that control spline<br>
that gives us three points ahead of our car from which we will generate our trajectory<br>
after having our trajectory, we break it into points that is accessible to the car within the acceleration and jerk limits based on our commanded velocity 'cmd_vel'.<br>
and that’s it!!
