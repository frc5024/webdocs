---
layout: default
title: "Common Sensors"
parent: "Learning"
permalink: /docs/learn/common-sensors
authors: ['ewpratten']
---

# Common sensors
This page was based off a guide from [Team 2605](https://seamonsters-2605.github.io/).

## Encoders

![encoder]

 - Measures rotation of motor shaft.
 - Connects to Talon, which tracks cumulative position and velocity.
 - RoboRIO requests and receives encoder data from Talon over CAN bus.

### Using Encoders

Encoders track the rotation and speed of the motor. They count upwards continuously as the motor rotates forwards and downwards as it rotates backwards. The Talon can try to approach a target position or velocity using encoders.

Methods for reading from an encoder attached to a TalonSRX:
 - `.configSelectedFeedbackSensor(FeedbackDevice.QuadEncoder, 0, 0)`: Required before using encoders. Tells the talon what type of encoder to check for.
 - `.getSelectedSensorPosition(0)`: Get the position of the encoder.
 - `.getSelectedSensorVelocity(0)`: Get the velocity of the encoder, in ticks per 100ms.

The talon.set function has an optional first argument that allows different control modes:
 - `.set(ControlMode.PercentOutput, speed)`: The default. Drive in voltage mode. Speed is any number between -1 (full speed backwards) and 1 (full speed forwards).
 - `.set(ControlMode.Position, position)`: move to an encoder position.
 - `.set(ControlMode.Velocity, speed)`: move at a target speed, in encoder ticks per 100ms.
 - `.config_kP/I/D/F(P, I, D)`: The PID values control how the talon tries to approach a position or speed. These take experimentation to figure out. Try an I value of 0 and a D value between 3 and 6, and adjust the P value to control how strongly the talon tries to approach a position (team 2605 has used P values anywhere from 0.15 to 30).

## navX
 - Measures acceleration and rotation of robot (6 axes).
 - Connects to RoboRIO via pin header.
  
### Using the navX
![navx]

The NavX is a device which detects movement and rotation of the robot. An “AHRS” object represents a reference to the NavX.

You will need to import the navX library: `import com.kauailabs.navx.frc.AHRS; `

Create an AHRS object: `AHRS m_gyro = new AHRS(Port.kMXP); `

`m_gyro.getAngle()`: Returns the total rotation of the robot in degrees. For example, if the robot rotates clockwise for 2 full rotations, this will be 720.

## Limelight
![limelight]

 - Tracks retroreflective vision targets.
 - Includes an LED array for illuminating target and a camera.
 - Onboard processor filters out and locates the target. Settings can be configured through a web interface.
 - Communicates with RoboRIO over ethernet, using the “NetworkTables” protocol.


<!-- Images -->
[encoder]: {{site.baseurl}}/assets/img/AMT103-V.jpg
{:width="250px"}

[navx]: {{site.baseurl}}/assets/img/navx.jpg
{:width="250px"}

[limelight]: {{site.baseurl}}/assets/img/limelight.jpg
{:width="250px"}