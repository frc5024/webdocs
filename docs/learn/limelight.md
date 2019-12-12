---
layout: default
title: "Limelight"
parent: "Learning"
permalink: /docs/learn/limelight
authors: ['slownie', 'ewpratten']
---

# What is a Limelight?
![Limelight Smart Camera]({{site.baseurl}}/assets/img/limelight.jpg)

[Limelight](https://limelightvision.io/) is a smart camera built for the FIRST Robotics Competition, and is a plug-and-play solution for vision on the robot. Vision takes a ton of time to incorporate on the robot and Limelight helps streamline this process, allowing us to focus on applying vision rather than coding it.

# How do I install the Limelight?
Usually we will leave this up to build, but sometimes we have to take matters into our own hands. There are three steps to setting up the Limelight: Mounting, Wiring, and Networking.

## Mounting
Use four 10-32 screws of 1 1/4" length and four nylock nuts to mount your Limelight.

## Wiring
Run two wires from your Limelight to a slot on your PDP, and add a 5A breaker. Finally, run an ethernet cable from your Limelight to your radio.
You could also run two wires to your PDP, and run an ethernet cable to your radio.

## Networking
Give the Limelight and a team number through its web interface at http://limelight.local:5801. The IP address for the Limelight is 10.50.24.11:5801.

The raw MJPEG video stream






 can be found on port `5800`.

# Programming
Although the Limelight handles the vision process, we still need the data from it. Lib5k's limelight component handles all the Networktable work.
``` java
import frc.lib5k.components.Limelight;

Limelight light = new Limelight();

//read if target is visible
boolean isVisible = Limelight.isTargetVisible();

//capture snapshot of target
LimelightTarget target = LimeLight.getTarget();

//read data from target
double x = target.getX();
double y = target.getY();
double s = target.getSkew();

//post to smart dashboard
SmartDashboard.putNumber("LimelightVisibility", isVisible);
SmartDashboard.putNumber("LimelightX", x);
SmartDashboard.putNumber("LimelightY", y);
SmartDashboard.putNumber("LimelightS", s);
```
For more information on the Limelight documentation, [click here](http://docs.limelightvision.io/en/latest/).

