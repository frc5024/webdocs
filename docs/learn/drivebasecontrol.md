---
layout: default
title: "Drivebase Control"
parent: "Learning"
permalink: /docs/learn/drivebasecontrol
authors: ['ewpratten']
---

# Drivebase Control from joystick inputs
Controlling a robot's movement with a joystick is a very common task for FRC. This document will outline some possible ways to convert joystick data to motor data. All examples assume a [tank-like](http://www.simbotics.org/resources/mobility/comparing-tank-drivetrains) drivebase, and that the joystick speed is represented by `double speed;` and rotational control by `double rotation;`.

## Rate-of-change control
The vast majority of FRC teams use rate-of-change calculation to control their robots, often without understanding how it works. To use rate-of-change control with your robot, use `DifferentialDrive.arcadeDrive(double,double);` in your code.

Rate-of-change control works by simply modifying speed by rotation:
```java
double left_motor_speed = speed + rotation;
double right_motor_speed = speed - rotation;
```

Below is a graph of motor speeds over input speed (form `-1.0` to `1.0`) assuming a `rotation` value of `0.45`.

![Rate-of-change graph]

The purple (top) line is the left motor output, and the black (bottom) line is the right output. 

## Constant-curvature control
![Constant-curvature graph]

## Hybrid control
![Hybrid graph]

### With deadbands

![Weighted hybrid graph]

![Very weighted hybrid graph]

## A comparison
![All control methods]


<!-- Images -->
[All control methods]: /webdocs/assets/img/all-control.png
{:width="300px"}

[Hybrid graph]: /webdocs/assets/img/hybrid-control.png
{:width="300px"}

[Constant-curvature graph]: /webdocs/assets/img/const-control.png
{:width="300px"}

[Rate-of-change graph]: /webdocs/assets/img/roc-control.png
{:width="300px"}

[Weighted hybrid graph]: /webdocs/assets/img/weighted-control.png
{:width="300px"}

[Very weighted hybrid graph]: /webdocs/assets/img/veryweighted-control.png
{:width="300px"}