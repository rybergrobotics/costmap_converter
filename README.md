Human detection module
=============================

### Proposal for human detection system
According to my understanding the ideal human detection system would have:
* 360 degrees coverage around the robot, so that it can detect humans that approach it from all sides.
* A max range of about 5 meters, since further away the intensity of UVC is minimal.
* Operation while the robot is moving.
* Close to zero false positives, since false positives would mean that the robot would need to stop it's normal operation.
* Close to zero false negatives, since false negatives would result in the robot not turning off the lamps while humans are nearby.
* Operation independent from environmental lightning conditions. (This places a hard restriction on camera based image recognition systems).
* Detection of both moving and stationary humans.

The three ways that I have tried so far to approach this problem have been the following:
* Using a motion detection sensor, similar to the ones used in building security. It could not work since the robot is moving and the self motion is detected. As a result, this method produces false positives, the moment the robot moves.
* Using a human detection neural network. This method, does not cover restriction #1 and is greatly complicated by #3 and #6. As a result a lot of false positives where produced. However, it is the only one that can potentially cover restriction #7.
* Using moving obstacle detection software. This method, does not cover restriction #7. However, it has the potential to cover every other one. 
Sadly, I have used three different moving obstacle detection systems and with not one of them, was I able to find a set of configuration settings that would give no false positives while the robot was moving. Since, these systems are intended for recognizing obstacles, false positives on moving obstacles are still stationary obstacles that need to be avoided.

In conclusion, I believe that building a human detection system, that covers all the above restrictions is extremely challenging with the current technology. 
What I propose as a technically viable alternative, would be a system that does not cover #3 and #7. This means, that we have moving human detection while the robot is stationary. 
This can be implemented by having the robot stop for 3-10 seconds after it reaches every waypoint and search for motion. If it does sense motion it closes the lights, otherwise it continues as normal.

### ROS API
Human detection are published in /uvc/humans

costmap_converter ROS Package
=============================

A ros package that includes plugins and nodes to convert occupied costmap2d cells to primitive types

Build status of the *master* branch:
- ROS Buildfarm Noetic: [![Noetic Build Status](http://build.ros.org/buildStatus/icon?job=Ndev__costmap_converter__ubuntu_focal_amd64)](http://build.ros.org/job/Ndev__costmap_converter__ubuntu_focal_amd64/)
- ROS Buildfarm Melodic: [![Melodic Build Status](http://build.ros.org/buildStatus/icon?job=Mdev__costmap_converter__ubuntu_bionic_amd64)](http://build.ros.org/job/Mdev__costmap_converter__ubuntu_bionic_amd64/)


### Contributors

- Christoph Rösmann
- Franz Albers (*CostmapToDynamicObstacles* plugin)
- Otniel Rinaldo


### License

The *costmap_converter* package is licensed under the BSD license.
It depends on other ROS packages, which are listed in the package.xml. They are also BSD licensed.

Some third-party dependencies are included that are licensed under different terms:
 - *MultitargetTracker*, GNU GPLv3, https://github.com/Smorodov/Multitarget-tracker
   (partially required for the *CostmapToDynamicObstacles* plugin)

All packages included are distributed in the hope that they will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the licenses for more details.



