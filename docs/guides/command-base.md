---
layout: default
title: "CommandBased Programming"
parent: "Guides"
permalink: /docs/guides/command-base
authors: ['ewpratten']
---

# CommandBased Programming
We use a modified version of WPIlib's CommandBase code structure. The first half of this guide will explain CommandBase to 1st and 2nd year programmers. With small corrections were we have changed functionality. The second half will explain our changes. This guide is partially based off of a guide from the [Toronto Coding Collective](https://www.torontocodingcollective.com).

## Objective of the Command Based Robot

WPILib supports a method of writing programs called "Command based programming". Command based programming is a design pattern to help you organize your robot programs. 

Some of the characteristics of robot programs that might be different from other desktop programs are:

 - Activities happen over time, for example a sequence of steps to shoot a Frisbee or raise an elevator and place a tube on a goal.
 - These activities occur concurrently, that is it might be desirable for an elevator, wrist and gripper to all be moving into a pickup position at the same time to increase robot performance.
 - It is desirable to test the robot mechanisms and activities each individually to help debug your robot.
 - Often the program needs to be augmented with additional autonomous programs at the last minute, perhaps at competitions, so easily extendable code is important.

Command based programming supports all these goals easily to make the robot program much simpler than using some less structured technique.

## Structure of the Software Layers
The Command Based Robot has the following structure:

![CommandBase structure diagram](/webdocs/assets/img/commandbase-structure.jpg)


### Operator Interface

The operator input defines the mapping between the operator physical device and the command layer.  When a button is pressed, the robot will take an action.  The OI layer allows for quick re-configuration of button actions.

### Commands

Commands are the glue in the robot connecting operator inputs to the robots motors and sensors.  A command will read the operator control inputs and subsystem sensors to determine the appropriate robot action.  Complex robot actions are performed though grouping of commands.

### Subsystems

Subsystems are containers for all of the motors, pneumatic actuators and sensors on the robot.  The subsystems provide feedback to the command layer, and take inputs from the command layer.

A correction to the diagram above: We do not support default commands. Our custom setup works on a "last in, first out" basis. This means that, in a case of conflicting control from commands, the last command to interact with a subsystem before the next loop will be the one that gets priority. 

## Commands

![Command structure diagram](/webdocs/assets/img/command.jpg)

Commands run over a subsystem or set of subsystems to coordinate specific actions.

Each subsystem has a default command, and that command typically takes user inputs from the Joysticks (or OI layer) and translates those actions into motor movements.  For instance, a typical DriveControl command reads Joystick values and sets the left and right motor speeds in a DriveTrain Subsystem.

In general, each command runs until it ends, or until it is interrupted by another command.  That means there could be several concurrently active commands running - one for each subsystem on the robot!

All currently active commands in the robot are called at approx 50Hz, or once every 20ms.  

## Our modifications
Much like a command, our subsystems are designed to run in their own loop. When programming the robot, make sure to use an `frc.lib5k.loops.loopables.LoopableSubsystem` class instead of the standard `edu.wpi.first.wpilibj.command.Subsystem`. The `LoopableSubsystem` will automatically handle it's loops in the background. Any code that reads from a sensor should happen in the `periodicInput` method, and any code that writes to an output should happen in the `periodicOutput` method.

An example `LoopableSubsystem` might look like this:
```java
package frc.robot.subsystems;

import frc.lib5k.loops.loopables.LoopableSubsystem;
import frc.lib5k.utils.RobotLogger;


public class MySubsystem extends LoopableSubsystem {
    RobotLogger logger = RobotLogger.getInstance();
    public static MySubsystem m_instance = null;

    public MySubsystem() {
        // Subsystem should be initialized here
    }

    /**
     * This is required for every Subsystem
     */
    public static MySubsystem getInstance() {
        if (m_instance == null) {
            m_instance = new MySubsystem();
        }

        return m_instance;
    }

    @Override
    public void periodicOutput() {
        // Here should be code that makes components move        
    }

    public void periodicInput() {
       // Here should be code that reads from any required sensor(s)
    }

    @Override
    public void outputTelemetry() {
        // Here should be code that pushes telemetry data to SmartDashboard
    }

    @Override
    public void stop() {
        // Here should be code that stops any moving component controlled by this subsystem
    }

    @Override
    public void reset() {
        stop();
        // Here should be code that resets all sensors needed by this subsystem
    }

}
```

To register this `LoopableSubsystem` with the `SubsystemLooper`, the Subsystem instance must be passed to the `register` method of the `SubsystemLooper`.