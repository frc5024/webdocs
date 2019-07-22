---
layout: default
title: "Multithreaded Programming"
parent: "Learning"
permalink: /docs/learn/threading
authors: ['ewpratten']
---

# Multithreaded Programming
Occasionally, it is useful to truly parallelize two pieces of code. For our usecase, this requirement is rare, but sometimes necessary.

Some multithreaded components of our robot code are:
 - The `robotPeriodic` loop
 - The `RobotLogger`'s output handling
 - The `SubsystemLooper` and, by proxy, all periodic methods of any `LoopableSubsystem`

When working on these systems, it is important to understand how to write threaded code for our robots.

## Notifiers
WPIlib provides a very useful helper class called a [`Notifier`](https://first.wpi.edu/FRC/roborio/release/docs/java/edu/wpi/first/wpilibj/Notifier.html), which allows easy creation and management of time-based threads.

A notifier, once created, will simply call the provided method once every `n` seconds. Just like the periodic loops in the `Robot` class.

Here is an example of a `Notifier`'s use in Java:
```java
import edu.wpi.first.wpilibj.Notifier;

public class MyThreadedClass{
    Notifier m_notifier;

    public MyThreadedClass(){
        // Configure the notifier to run the doThing method
        m_notifier = new Notifier(this::doThing);

        // Start the notifier to run doThing every 20ms
        m_notifier.startPeriodic(0.02);
    }

    // Method that we want to be run in it's own thread
    private void doThing(){
        // We do something here
    }
}
```

Note, when specifying the method to run, we need to use `this::` followed by the name of the method. This passes the method as a `Runnable` to the `Notifier`. To stop this thread, we simply need to call `m_notifier.stop()`.

## True Threading
Using threads without a wrapper can be very dangerous, but may be needed. Here is an example of a *normal* thread:
```java
public class Robot extends IterativeRobot {
    public void robotInit() {
        Thread t = new Thread(() -> {
        while (!Thread.interrupted()) {
            // Do the thing here
            }
        });t.start();
    }
}
```