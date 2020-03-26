---
layout: default
title: "CommandBased Programming"
parent: "Guides"
permalink: /docs/guides/command-base
authors: ['ewpratten']
---

# CommandBased Programming
We use WPIlib's CommandBase code structure. The first half of this guide will explain CommandBase to 1st and 2nd year programmers. The second half of this guide will explain how to implement them. This guide is partially based off of a guide from the [Toronto Coding Collective](https://www.torontocodingcollective.com).

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


## Implementation
There are two seperate classes need to make a command and a subsystem to make a command a programmer must extend `edu.wpi.first.wpilibj2.command.CommandBase` in the class they wish to make a command, To create a subsystem the class must extend `edu.wpi.first.wpilibj2.command.SubsystemBase`. This gives access to the methods needed to create a functioning command and a functioning subsystem.


An example `SubsystemBase` might look like this:
```java
package frc.robot.subsystems;

import edu.wpi.first.wpilibj2.command.SubsystemBase;
import frc.robot.OI;
import edu.wpi.first.wpilibj.Talon;


public class ExampleSubsystem extends SubsystemBase{
    private static ExampleSubsystem instance = null;
    private OI oi = OI.getInstance();
    Talon talon1;

    // Code made when subsystem is created
    private ExampleSubsystem(){
        talon1 = new Talon(0);
    }

    // Create a Singleton
    public static ExampleSubsystem getInstance(){

        if(instance == null){
            instance = new ExampleSubsystem();

            return instance;
        }

        return instance;
    }

    // Creates a Periodic loop that runs at 50hz
    @Override
    public void periodic(){
        // Checks OI to see if motor should be on
        if(oi.shouldTurnOn()){
            talon1.set(.5);
        }else{
            talon1.stopMotor();
        }
    }

}
```
To register this Subsystem, the Subsystem instance must have it the register method called on it.


An example `CommandBase` might look like this:
```java
package frc.robot.subsystems;

import edu.wpi.first.wpilibj.Talon;
import edu.wpi.first.wpilibj2.command.CommandBase;


public class ExampleCommand extends CommandBase{
    Talon talon1 = new Talon(0);

    
    // When the command starts set safety to false
    @Override
    public void initialize() {
        talon1.setSafetyEnabled(false);
    }

    // Each loop increase the motor speed by .1
    @Override
    public void execute() {
        talon1.setSpeed(talon1.getSpeed() + .1);
    }

    // When the commands end set speed to zero and enable safety
    @Override
    public void end(boolean interrupted) {
        talon1.setSpeed(0);
        talon1.setSafetyEnabled(true);
    }

    // if the motor is at 1 speed stop the command, otherwise continue
    @Override
    public boolean isFinished() {
        if(talon1.getSpeed() == 1){
            return true;
        }else{
            return false;
        }
    }

}
```