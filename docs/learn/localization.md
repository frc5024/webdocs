---
layout: default
title: "Robot Localization"
parent: "Learning"
permalink: /docs/learn/localization
authors: ['ewpratten']
---

# [WIP] Robot Localization
Localization is like a GPS for our robots. We use a group of precise sensors to determine the robot's location withing a few centimeters accuracy. 

## Available implementations
There are many ways to determine a robot's location on the field. Some are much easier to accomplish than others. Here are a few common methods:

 - Adding a light beacon to the robot, then using computer vision from a camera on the DriverStation to find the robot's rough location
   - 254 used [a similar technique](https://github.com/Team254/FRC-2018-Public/blob/2c06c1ea5c81b6ed970fa8bc2611f69467a08075/dash/CheesyVision2.py#L73-L208) to determine the scale's height in for their 2018 robot, [Lockdown](https://www.team254.com/first/2018/)
 - Using RFID beacons
   - Requires support from the venue & field
   - Provided by [Zebra Technologies](http://indianaroboticsinvitational.org/zebra-technologies/) for some FRC events
 - Using an overhead camera view to detect robot position
   - Similar concept to the first option
   - Not currently FRC field legal
 - Using encoders & gyroscopes to track location history
   - Requires precise sensors, and reliable code
   - Can run anywhere without needing external sensors (cameras, radios)
   - Used by many teams, and [well documented](https://web.wpi.edu/Pubs/E-project/Available/E-project-042418-200712/unrestricted/final_report.pdf)

## Our implementation


### Angle offset