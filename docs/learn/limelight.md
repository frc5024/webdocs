---
layout: default
title: "Limelight"
parent: "Learning"
permalink: /docs/learn/limelight
authors: ['slownie']
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

## Networking
Give the Limelight and a team number through its web interface at http://limelight.local:5801. 

# Programming
Although the Limelight handles the vision process, we still need the data from it. Read the document on [Network Tables](/docs/learn/networking-tables) to understand the programming section.

``` java
import edu.wpi.first.wpilibj.smartdashboard.SmartDashboard;
import edu.wpi.first.networktables.NetworkTable;
import edu.wpi.first.networktables.NetworkTableEntry;
import edu.wpi.first.networktables.NetworkTableInstance;

NetworkTable table = NetworkTableInstance.getDefault().getTable("limelight");
NetworkTableEntry tx = table.getEntry("tx");
NetworkTableEntry ty = table.getEntry("ty");
NetworkTableEntry ta = table.getEntry("ta");

//read values periodically
double x = tx.getDouble(0.0);
double y = ty.getDouble(0.0);
double area = ta.getDouble(0.0);

//post to smart dashboard periodically
SmartDashboard.putNumber("LimelightX", x);
SmartDashboard.putNumber("LimelightY", y);
SmartDashboard.putNumber("LimelightArea", area);