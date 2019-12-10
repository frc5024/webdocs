---
layout: default
title: "Extended TimedRobot"
parent: "Lib5K Reference"
permalink: /docs/lib5k/timedrobot-ext
authors: ['ewpratten']
---

# The extended TimedRobot framework

WPILib provides a very useful `TimedRobot` framework, but there are a few extra features we would like to add. These are provided by Lib5K's `TimedRobotEXT` class. Keep in mind, `TimedRobotEXT` extends `TimedRobot`, so all [TimedRobot methods](https://first.wpi.edu/FRC/roborio/release/docs/java/edu/wpi/first/wpilibj/TimedRobot.html) are still available.

## SharedInit

Sometimes, we need code to be run on both `teleopInit` and `autonomousInit` (for example, starting drive code during sandstorm in 2019). This can be done with the `sharedInit` method.

```java
import frc.lib5k.framework.TimedRobotEXT;

public class Robot extends TimedRobotEXT{

    @Override
    public void sharedInit(){
        // Shared code goes here
        ...
    }

    @Override
    public void autonomousInit(){
        // Call shared init
        sharedInit();

        // do other stuff
        ...
    }

    @Override
    public void teleopInit(){
        // Call shared init
        sharedInit();

        // do other stuff
        ...
    }
}
```

## RobotStateHandler

Sometimes, a subsystem requires code to be run on robot enable and disable. This can be done with a `RobotStateHandler`. This will provide two methods that will be run on robot state change (enable and disable).

```java
// MySubsystem.java

public class MySubsystem extends Subsystem implements RobotStateHandler{

    // Subsystem code here
    ...

    // Robot enable handler
    @Override
    public void onEnable(){
        
        // This code will be run when the robot is enabled
        ...
    }

    // Robot disable handler
    @Override
    public void onDisable(){
        
        // This code will be run when the robot is disabled
        ...
    }
}

```

This code will not run by itself. The subsystem must be registered with the robot upon creation.


```java
// Robot.java
// This is an extension of the example above

import frc.lib5k.framework.TimedRobotEXT;

public class Robot extends TimedRobotEXT{

    MySubsystem sys = new MySubsystem();

    @Override
    public void robotInit(){
        // Register the subsystem for state handling
        registerStateHandler(sys);

    }

    @Override
    public void sharedInit(){
        // Call handlers
        handleRobotEnable();
        
        // Shared code goes here
        ...
    }

    @Override
    public void autonomousInit(){
        // Call shared init
        sharedInit();

        // do other stuff
        ...
    }

    @Override
    public void teleopInit(){
        // Call shared init
        sharedInit();

        // do other stuff
        ...
    }

    @Override
    public void disabledInit(){
        // Call handlers
        handleRobotDisable();
    }
}
```