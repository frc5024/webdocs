---
layout: default
title: "RobotLogger"
parent: "Lib5K Reference"
permalink: /docs/lib5k/robotlogger
authors: ['ewpratten']
---

# RobotLogger
The RobotLogger is a threaded logging system that reduces stress on the network logging system (NetConsole), and reduces console spam.

## Logging
To log data with the RobotLogger, You can do the following in any class
```java
// Get a logger instance
RobotLogger logger = RobotLogger.getInstance();

// Log some standard text
logger.log("Some text");

// Log a warning
logger.log("This is a warning", Level.kWarning);

// Log data before the scheduler starts
logger.log("This will be immediately pushed to the console", Level.kRobot);
```

## Stating the logger
The RobotLogger must be started when the robot is initialized.

```java
class Robot{
    RobotLogger logger = RobotLogger.getInstance();

    void robotInit(){
        logger.start(0.02);
    }
}
```

`logger.start()` must be passed a loop period. This should be the same as the robot period (by default `0.02`).

## How it works
The RobotLogger uses an `ArrayList` to buffer any message to be logged, then upon a call to `update` (usually by the FRC Notifier), it will print every message from the list and clear it. 

Any message logged at the `Level.kRobot` level, will be immediately pushed to the console.

