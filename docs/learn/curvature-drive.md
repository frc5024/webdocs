---
layout: default
title: "Curvature Drive"
parent: "Learning"
permalink: /docs/learn/curvature-drive
authors: ['hyperliskdev']
---

# Curvature Drive

Curvature drive is a method inside of the DifferentialDrive class in WPILib 

## What does Curvature Drive do?

Curvature drive is a type of drive just like Arcade or Tank drive. Curvature drive is different in a few key ways;

- isQuickTurn method is used to quickturn on the stop, as it is default off.
- Turning speed withput isQuickTurn == true, is based on how fast the robot is moving.
- The robot can be driven with either Trigger Control or Joystick Control
- And finally, the robot now drives like a car.

## How to make Curvature drive

```java

// Inside DriveTrain.java (hyperliskdev/HyperBot)

public void curvDrive(double speed, double rotation, boolean isQuickTurn) {

    m_DifferentialDrive.curvatureDrive(speed, rotation, isQuickTurn);
    
    
  }
```

Is moving isnt required but could be helpful in auto or for something else ive never heard of.

Inside the drive controller class:

``` java
// Called repeatedly when this Command is scheduled to run
  @Override
  protected void execute() {


    // Main vars for driving.
    speed = Robot.m_oi.getTriggerThrottle();
    rotation = Robot.m_oi.getRotation();
    isQuickTurn = Robot.m_oi.getQuickTurn();

    // Deadbanding stuff
    speed = m_speedDeadband.feed(speed);
    rotation = m_rotationDeadband.feed(rotation);

    // Calling the function created in DriveTrain.java
    Robot.m_driveTrain.curvDrive(speed, rotation, isQuickTurn);

  }

```

getTrigger will return a value from 0 --> 1 based on how far down the trigger is pressed. <br>
getRotation will return a value from -1 --> 0 --> 1, based on where the joystick is in relation to the center <br>
quickTurn will let the Robot turn without speed. <br>

If quickTurn is not enabled, the robot will not turn unless it is moving.
When the robot is moving, it will only turn based on how fast it is moving.
Spesifically, this fast

``` java 

if (isQuickTurn) {
      if (Math.abs(xSpeed) < m_quickStopThreshold) {
        m_quickStopAccumulator = (1 - m_quickStopAlpha) * m_quickStopAccumulator
            + m_quickStopAlpha * limit(zRotation) * 2;
      }
      overPower = true;
      angularPower = zRotation;
    } else {
      overPower = false;
      angularPower = Math.abs(xSpeed) * zRotation - m_quickStopAccumulator;

      if (m_quickStopAccumulator > 1) {
        m_quickStopAccumulator -= 1;
      } else if (m_quickStopAccumulator < -1) {
        m_quickStopAccumulator += 1;
      } else {
        m_quickStopAccumulator = 0.0;
      }
    }

```
angularPower is a double, that; if IsQuickTurn is true, will be default set to the rotation given. <br>
if not; the angularPower is set to the absolute value of speed * rotation - this weird quickStopAccumulator. <br>
The quickstop accumulator isnt actually, initalized inside of DifferrentialDrive so i have no clue what that value is doing... <br>
