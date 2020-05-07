---
layout: default
title: "GearBox"
parent: "Lib5K Reference"
permalink: /docs/lib5k/gearbox
authors: ['ewpratten']
---

# GearBox
A GearBox is a wrapper for any collection of motor controllers. Currently, the only supported controller is the [CTRE TalonSRX](http://www.ctr-electronics.com/talon-srx.html).

## Creating a GearBox
To create a GearBox, pass in a pair of `WPI_TalonSRX` objects, and a `boolean` to specify if the sensor is attached to the rear (second) motor or not.
```java
// Create a GearBox with talons 1 & 2, and an encoder attached to talon 1
GearBox myGearbox = new GearBox(new WPI_TalonSRX(1), new WPI_TalonSRX(2), false);

// Create a GearBox with talons 1 & 2, and an encoder attached to talon 2
GearBox myGearbox = new GearBox(new WPI_TalonSRX(1), new WPI_TalonSRX(2), true);
```

This will create, and connect to both motor controllers, automatically configure them, and pair them together to follow eachother.

## Configuring current limiting
Limiting the maximum output current of a motor is very useful. It allows systems to operate together without browning out the robot. To configure current limiting on a GearBox, use the `limitCurrent` method.
```java
// Configure the current limits with a trigger of 32Amps, a hold at 30Amps, and a duration of 15
myGearbox.limitCurrent(32, 30, 15);
```

The peak / trigger current is the number of [Amperes](https://en.wikipedia.org/wiki/Ampere) the system must draw before the limiter takes effect.

The current hold is the maximum number of Amperes the system can draw once the peak / trigger has been tripped.

The duration is the amount of time the system's current draw must exceed the peak (in ms) before the limit takes effect.

## Directly controlling
To directly control the GearBox, use the `set` method. This will set the motor output percentage.
```java
// Output full speed forwards
myGearbox.set(1.0);

// Output full speed beckwards
myGearbox.set(-1.0);
```

## Using with `DifferentialDrive`
Our robot's [drivetrains](https://en.wikipedia.org/wiki/Drivetrain) usually have at least 2 motors per side. This allows the use of a GearBox to "package" each motor group together, and pass to WPIlib's [DifferentialDrive](https://first.wpi.edu/FRC/roborio/release/docs/java/edu/wpi/first/wpilibj/drive/DifferentialDrive.html) controller. To build a DifferentialDrive from two gearboxes (with two motors each), the following can be done:
```java
// Create a GearBox for each side of the robot
GearBox leftGearbox = new GearBox(new WPI_TalonSRX(1), new WPI_TalonSRX(2), false);
GearBox rightGearbox = new GearBox(new WPI_TalonSRX(3), new WPI_TalonSRX(4), false);

// Create the DifferentialDrive object
DifferentialDrive drive = new DifferentialDrive(leftGearbox.getMaster(), rightGearbox.getMaster());
```

All regular DifferentialDrive functionality will now work with these motors.

## Reading sensors
Each GearBox will allow an [encoder](/webdocs/docs/learn/common-sensors#encoders) to be attached to one of the talons. (make sure to specify which one with the boolean in the GearBox constructor).

To read the number of ticks from a GearBox's encoder, use it's `getTicks` method.
```java
// Read the tick count of a GearBox encoder
int ticks = myGearbox.getTicks();
```

### The GearBoxEncoder
Lib5K also includes an [EncoderBase](/webdocs/docs/lib5k/encoderbase). This is a single class that can adapt any type of encoder into a unified interface. To create one from a GearBox, the `GearBoxEncoder` wrapper can be used.

```java
// Create an EncoderBase from a GearBox
EncoderBase myEncoder = new GearBoxEncoder(myGearBox);
```

Now, additional data can be read from the encoder.
```java
// Get the GearBox output speed in Ticks per second
double speed = myEncoder.getSpeed();

// Get the distance traveled in meters (this requires information about the GearBox's output)
// This example will use the parameters of one of MiniBot's wheels
double distance = myEncoder.getMeters(720, (6.0*2.54) * Math.PI);
```

**Don't forget to call the EncoderBase's `update` method from inside the DriveTrain's Subsystem!**