---
layout: default
title: "Curvature Drive"
parent: "Learning"
permalink: /docs/learn/curvature-drive
authors: ['hyperliskdev', 'ewpratten']
---

# Constant Curvature Drive

Curvature Drive is a method inside of DifferentialDrive that is similar to Arcade Drive or Tank Drive. All of these methods complete the same basic function; sending information's to the motors on how much to move and in which direction. 

## What does constant curvature mean?
Constant Curvature drive controls the robot path's curvature instead of its rate-of-change, like ArcadeDrive does. In ArcadeDrive, it is possible for the robot to turn on the spot. Whereas, with curvature drive, this is not possible.

A real-world example of constant-curvature control is a car. A car's ability to turn is dependant on it's velocity. The same is true of curvature drive.

![Constant-curvature graph]

This graph depicts the left, and right motor outputs over the robot's velocity with a constant turning factor.


## Cheesy Drive

Developed by Team 254, Cheesy Drive's earliest recorded use case is in the 2014 source code for the game Aerial Assist. Cheesy Drive sparked the interest of WPI and they implemented a version of it, calling it simply Curvature Drive. 

This following snippet from the CheesyPoofs' 2016 codebase explains cheesy drive in a very simplistic way.

``` java
/**
 * Helper class to implement "Cheesy Drive". "Cheesy Drive" simply means that
 * the "turning" stick controls the curvature of the robot's path rather than
 * its rate of heading change. This helps make the robot more controllable at
 * high speeds. Also handles the robot's quick turn functionality - "quick turn"
 * overrides constant-curvature turning for turn-in-place maneuvers.
 */
```

## When to use curvature drive

Curvature Drive could be use in many places. Strategy wise, Curvature Drive is best suited for getting across the field as fast as possible. Its usability at higher speeds makes it great for putting the pedal to the metal and the availability of quickTurn makes it great when making small adjustments to placement of game pieces.  

## How do I use it?
Since the implementation into DifferentialDrive, it is as easy as using arcadeDrive. 

First step is to make a method in your drivetrain class.
``` java

  // Curvature Drive Mode
  public void curvDrive(double speed, double rotation, boolean isQuickTurn) {
    isMoving = (speed != 0.0);
    isTurning = (rotation != 0.0);

    m_DifferentialDrive.curvatureDrive(speed, rotation, isQuickTurn);
    
  }

```

Step two, create varibles inside drive controller class.

``` java 

public class DriveControl extends Command {

    // Movement vectors
  double speed, rotation = 0.0;
  boolean isQuickTurn;

 //...
 // Called repeatedly when this Command is scheduled to run
  @Override
  protected void execute() {


    // Main vars for driving.
    speed = Robot.m_oi.getTriggerLeftThrottle();
    rotation = Robot.m_oi.getRotation();
    isQuickTurn = Robot.m_oi.getQuickTurn();

```


Step three, call the curvature drive method inside drive control.

``` java

// Called repeatedly when this Command is scheduled to run
  @Override
  protected void execute() {


    // Main vars for driving.
    speed = Robot.m_oi.getTriggerLeftThrottle();
    rotation = Robot.m_oi.getRotation();
    isQuickTurn = Robot.m_oi.getQuickTurn();
    
    // Deadbanding stuff
    // speed = m_speedDeadband.feed(speed);
    rotation = m_rotationDeadband.feed(rotation);

    Robot.m_driveTrain.curvDrive(speed, rotation, isQuickTurn);
    
  }

```

Deploy and ``` winGame(); ```

<!--- Images --->
[Constant-curvature graph]: /webdocs/assets/img/const-control.png
{:width="300px"}