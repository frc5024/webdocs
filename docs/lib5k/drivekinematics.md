---
layout: default
title: "Drivebase Kinematics"
parent: "Lib5K Reference"
permalink: /docs/lib5k/drivekinematics
authors: ['ewpratten']
---
(From java package `lib5k.kinematics`)

# Drivebase Kinematics
*"Kinematics is a branch of classical mechanics that describes the motion of points, bodies, and systems of bodies without considering the forces that cause them to move"* -[Wikipedia](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=36&cad=rja&uact=8&ved=2ahUKEwjEn-br7rjlAhWLVN8KHd5XAhcQmhMwI3oECAwQAg&url=https%3A%2F%2Fen.wikipedia.org%2Fwiki%2FKinematics&usg=AOvVaw3YJtWrMC7FfLS617mwvRLg)

Kinematics is very helpful for controlling, and defining robot movement during the autonomous period, along with various other in-game actions. This document will outline how we have integrated both forward, and inverse kinematics into Lib5K, and how to use these features in your robot program.

## Robot Localization
Robot localization, a form of forward kinematics, is the process of locating a robot in 2D or 3D space using a variety of sensors. Think of it like a GPS.

### Localization with an FRC robot
Assuming a [kitbot](https://www.andymark.com/products/am14u3-kop-chassis)-style drivetrain, we can use three simple sensors, and some trigonometry to determine the robot's location on the field with reasonable precision.

We need to know three things about the robot.
 - Total distance traveled
 - Current heading
 - Circumference of the wheels in meters

With this information, we can get an X, and Y coordinate of the robot in meters with the following code:
```java

// For storing the robot position
double x,y = 0.0;
double lastPos = 0.0;

// Calculate the circumference in meters of the wheels
// This assumes 6.0 inch wheels on the drivebase
final double wheelCirc = (6.0 * 0.0254) * Math.PI;

// Number of encoder ticks produced per wheel revolution
final int ticksPerRev = 720;

/**
 * Will convert an encoder tick count to a distance traveled in meters
 */
double ticksToMeters(int tickCount){
    return (tickCount / ticksPerRev) * wheelCirc;
}

/**
 * This should be called once per 20ms (or the robot periodic loop)
 */
void loop(){
    // Read the robot's current angle from the gyroscope and bind it by 360 degrees
    double heading = getAngle() % 360;

    // Find the average distance traveled between each side of the robot. This
    // will give the total Y distance traveled by the robot, accounting for rotation
    double leftMeters = ticksToMeters(getLeftEncoderTicks());
    double rightMeters = ticksToMeters(getRightEncoderTicks());

    double position = (leftMeters + rightMeters) / 2.0;

    // Find the distance traveled by the robot since the last time loop() was called
    double distance = position - lastPos;

    // Calculate position
    x += (distance * Math.cos(Math.toRadians(heading)));
    y += (distance * Math.sin(Math.toRadians(heading)));

    // re-set the last position
    lastPos = position;
}

```

This example assumes that the robot's heading / angle can be read with `getAngle()`, and each encoder has a method to read its tick count. If using the tools built in to Lib5K, all of this is handled for you.

#### How it works
Finding the robot location is relatively simple with the help of some trigonometry. 

![Field diagram with triangle to show how location is calculated](/webdocs/assets/img/loc-diag.jpg)

This diagram roughly demonstrates how location is calculated. In practice, calling the `loop()` method in a loop would generate a very large number of triangles, and provide much greater precision.

The diagram shows the calculation that would be completed if the robot started on HAB1 (at the red angle), and moved to the left rocket, then called `loop()` once. The robot's heading would be treated as *theta* (the red angle), and it's total distance traveled since the last loop as the *hypotenuse*. The labeled `X` and `Y` axis of the right-angled triangle are now the robot's `X,Y` location on the field.

### Lib5K LocalizationEngine
Lib5K provides a tool called the `LocalizationEngine`. This tool wil automatically complete the localization calculations, and convert the data to a `FieldPosition` object for easy use with other Lib5K tools and components, like the `MovementPlanner`.

#### Using it in your code
The `LocalizationEngine` requires some other components to work. The below example will assume you are using a robot similar to [MiniBot](/webdocs/docs/robots/minibot).

To use the `LocalizationEngine`, the same three sensors from the example above are required. Here, we will define our motors, their encoders, and a Gyroscope object. This code should be part of the DriveTrain subsystem.
```java
// Create two gearboxes with encoders attached to the rear motor controllers
GearBox leftGearbox = new GearBox(new WPI_TalonSRX(1), new WPI_TalonSRX(2), true);
GearBox rightGearbox = new GearBox(new WPI_TalonSRX31), new WPI_TalonSRX(4), true);

// Create two encoders from each gearbox
EncoderBase leftEncoder = new GeaBoxEncoder(leftGearbox);
EncoderBase rightEncoder = new GeaBoxEncoder(rightGearbox);

// Create a gyroscope (this example wil use a NavX)
AHRS gyro = new AHRS(Port.kMXP);
```

We additionally will need to get a `LocalizationEngine` instance to work with
```java
// Get the current LocalizationEngine instance
LocalizationEngine le_instance = LocalizationEngine.getInstance();
```

The codebase should have these values defined elsewhere (e.g. in the `Constants.java` file), but for this example, we will define a few parameters of the robot here:
```java
// Calculate the circumference in meters of the wheels
// This assumes 6.0 inch wheels on the drivebase
final double wheelCirc = (6.0 * 0.0254) * Math.PI;

// Number of encoder ticks produced per wheel revolution
final int ticksPerRev = 720;
```

Next, in the subsystem's `periodic()` method, or any other constantly looping method, we can update the `LocalizationEngine`
```java
@Override 
public void periodic(){
    // Get the robot heading
    double heading = gyro.getAngle();

    // Get each encoder's distance reading
    double leftMeters = leftEncoder.getMeters(ticksPerRev, wheelCirc);
    double rightMeters = rightEncoder.getMeters(ticksPerRev, wheelCirc);

    // Update the LocalizationEngine
    le_instance.calculate(leftMeters, rightMeters, heading);
}
```

The robot's position will now be constantly updated. At the start of autonomous, you may want to reset the robot's location. 
```java
// Set the robot's field-relitive location in meters.
// This example uses an X of 0, and a Y of 5 meters.
// This should be called at the start of each autonomous
// commandgroup to set the location appropriately.
le_instance.setRobotPosition(new FieldPosition(0.0, 5.0));
```

Finally, to read the robot's current location (and heading), the following can be done:
```java
FieldPosition currentPosition = le_instance.getRobotPosition();
```