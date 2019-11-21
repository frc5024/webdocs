---
layout: default
title: "Network Tables"
parent: "Learning"
permalink: /docs/learn/networktables
authors: ["wm-c", "rsninja722", "catarinaburghi"]
---

## What is A Network Table
A Network Table is a table of values that can be access by multiple devices over a network.

Data in a Network Table is arranged with a key and value

A key can have another table as its value

A Network Table can be used to update a device very quickly after the data has been written

## What can it be used for
A Network Table can be used to quickly share live data between different nodes on a network.

It can be used to
* Share live data about the Position of the robot
* Share the information of sensors and their value
* Share a set a data using an indented table


## Structure
The data must be stored as boolean with double precision, numeric, or string. You can have arrays of those types of data. There is also the option of storing raw data. 

## Example
```java
package edu.wpi.firstwpilibj.templates;

import edu.wpi.first.wpilibj.timedrobot;
import edu.wpi.first.networktables.NetworkTable;
import edu.wpi.first.networktables.NetworkTableEntry;
import edu.wpi.first.networktables.NetworkTableInstance;

public class EasyNetworkTableExample extends timedrobot{
    NetworkTableEntry yEntry;
    NetworkTableEntry xEntry;
    public void robotInit(){
        NetworkTableInstance inst = NetworkTableInstance.getDefault();
        Network table = inst.getTable("datatable");
        xEntry = table.getEntry("X")
        yEntry = table.getEntry("Y")
    }

    double x = 0;
    double y = 0;

    public void teleopPeriodic(){
        xEntry.setDouble(x);
        yEntry.setDouble(y);
        x += 0.05;
        y += 1.0;
    }
}
```



