---
layout: default
title: "Command Groups"
parent: "Guides"
permalink: /docs/guides/commandgroups
authors: ['',''slownie]
---

# Command Groups


## Sequential and Parallel Commands
When you add a command to the command group, it can be executed in two different ways; Sequential and Parallel. Sequential commands wait until they are finished (isFinished method returns true) before running the next command in the group. 

Parallel commands start running, then immediately schedule in the next command in the group. It is important to know which type to use when building a command group.

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

