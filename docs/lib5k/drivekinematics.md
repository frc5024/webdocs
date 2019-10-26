---
layout: default
title: "Drivebase Kinematics"
parent: "Lib5K Reference"
permalink: /docs/lib5k/drivekinematics
authors: ['ewpratten']
---

# Drivebase Kinematics
*"Kinematics is a branch of classical mechanics that describes the motion of points, bodies, and systems of bodies without considering the forces that cause them to move"* -[Wikipedia](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=36&cad=rja&uact=8&ved=2ahUKEwjEn-br7rjlAhWLVN8KHd5XAhcQmhMwI3oECAwQAg&url=https%3A%2F%2Fen.wikipedia.org%2Fwiki%2FKinematics&usg=AOvVaw3YJtWrMC7FfLS617mwvRLg)

Kinematics is very helpful for controlling, and defining robot movement during the autonomous period, and for various other in-game actions. This document will outline how we have integrated both forward, and inverse kinematics into Lib5K, and how to use these features in your robot program.

## Robot Localization
Robot localization is the process of locating a robot in 2D or 3D space using a variety of sensors. Think of it like a GPS.

### Localization with an FRC robot
Assuming a [kitbot](https://www.andymark.com/products/am14u3-kop-chassis)-style drivetrain, we can use three simple sensors, and some trigonometry to determine the robot's location on the field with reasonable precision.

We need to know three things about the robot.
 - Total distance traveled
 - Current heading
 - Circumference of the wheels in meters

With this information, we can get an X, and Y coordinate of the robot in meters by doing the following:
```java
double x,y = 0.0;

/**
 *
 */
void loop(){
    // Read the robot's current angle from the gyroscope and bind it by 360 degrees
    double angle = getAngle() % 360;
}

```

### Lib5K LocalizationEngine

#### Using it in your code