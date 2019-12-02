---
layout: default
title: "Curvature Drive"
parent: "Learning"
permalink: /docs/learn/curvature-drive
authors: ['hyperliskdev']
---

# Constant Curvature Drive

Curvature Drive is a method inside of DifferentialDrive that is similar to Arcade Drive or Tank Drive. All of these methods complete the same basic function; sending information's to the motors on how much to move and in which direction. 

## What does constant curvature mean?
Constant Curvature drive is different than arcade drive mainly because of what the name entails. The main goal of Constant Curvature Drive is to control curvature instead of rate-of-change, like in Arcade Drive. Arcade drive, it is possible to turn on the spot. Inversely, Curvature Drive you can. 

In a car, dependant on how fast you're going will determine how quickly you are able to turn. going slower leading to a slower turning speed and faster you can turn more quickly. This is what curvature drive is replicating.

![Constant-curvature graph]


## Cheesy Drive?

Developed by Team 254, Cheesy Drive's earliest recorded use case is in the 2014 source code for the game Aerial Assist. Cheesy Drive sparked the interest of WPI and they implemented a version of it, calling it simply Curvature Drive. It appears they built a Helper class to explain what Cheesy Drive is and to do math on what power to send to the PWM.


The 2016 CheesyPoofs code explains curvature drive in a very simplistic way.

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