---
layout: default
title: "Command Groups"
parent: "Guides"
permalink: /docs/guides/commandgroups
authors: ['catarinaburghi','slownie']
---

# Command Groups
This guide is based off of the offical WPILib documentation which can be found [here](https://wpilib.screenstepslive.com/s/currentCS/m/java/l/599738-creating-groups-of-commands).

Once you have created commands to operate the subsystems in your robot, they can be grouped together to get more complex operations. These groups are called Command Groups. An example of a Command Group would be the following:
```java
public class GrabBall extends CommandGroup {
    public GrabBall() {
        addSequential(new SetElevatorSetpoint(Elevator.TABLE_HEIGHT));
        addSequential(new SetWristSetPoint(Wrist.PICKUP));
        addSequential(new OpenClaw());
    }
}
```
This is an example of a command group that places a ball on a table. To accomplish this task, the robot has to set the elevator's destination (top of the table), then set it's wrist position, and finally open it's claw and pick up the ball. While this can all be done without the use of command groups, it's much easier and cleaner to create command groups.

## When do we use Command Groups
Command Groups can be used in two different ways, for autonomous or to automate sequences for the drivers. 

## Sequential and Parallel Commands
When you add a command to the command group, it can be executed in two different ways; Sequential and Parallel. Sequential commands wait until they are finished (isFinished method returns true) before running the next command in the group. Parallel commands start running, then immediately schedule in the next command in the group. It is important to know which type to use when building a command group. 

## How to create a Command Group
The code for creating a Command Group is the following:
```java
public class ExampleCommandGroup extends CommandGroup {
    public ExampleCommand() {
    	addSequential(new ExampleCommandOne());
    	addParallel(new ExampleCommandTwo());
    }
}
```

