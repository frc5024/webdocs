---
layout: default
title: "Your First Program"
parent: "Learning"
permalink: /docs/learn/your-first-program
authors: ['ewpratten']
---

# Writing your first robot program
This lesson assumes that you have already installed the FRC [development tools]({{site.baseurl}}/docs/guides/installing-tools) on your computer, or you are using a computer provided by the team. 

Open Visual Studio Code, and follow [WPIlib's instructions](https://frc-docs.readthedocs.io/en/latest/docs/software/wpilib-overview/creating-robot-program.html#creating-a-new-wpilib-project) for starting a new project. Make sure to set the team number to `5024`, Java as your programming language, and `Command Robot` as your template.

We will be writing a simple tank drive with two wheels, one on each side of the robot. Here is a visual:
![Team 2605's Tank drive visual]({{site.baseurl}}/assets/img/tank-drive.png)


## Preparing the project
WPIlib adds some extra template code to a new project to help teams out. We will not be needing that.

Start by deleting all the files inside of `src/main/java/frc/robot/subsystems`, then the same for `src/main/java/frc/robot/commands`.

Next, replace the contents of `src/main/java/frc/robot/Robot.java` with the following code:
```java
package frc.robot;

import edu.wpi.first.wpilibj.TimedRobot;
import edu.wpi.first.wpilibj.command.Scheduler;


public class Robot extends TimedRobot {
  
  public static OI m_oi;

  @Override
  public void robotInit() {
    m_oi = new OI();
    
  }

  @Override
  public void teleopInit() {
    
  }


  @Override
  public void teleopPeriodic() {
    Scheduler.getInstance().run();
  }


}

```

You now have a blank slate of a class. The `Robot` class is automatically called by the robot's hyperviser code running on the RoboRIO. You do not need to worry about how this works, as it is automatic.

## What do we want to do?
Deciding what to do with a robot is hard. Luckily, our testing robot has some wheels (as described above). So let's write some code to make our bot move.

## Controls
Firstly, we should start off with some controls. Our drive team uses Xbox controllers to drive our robots, so we will be writing some code for one of these controllers. To drive our bot, we will be using just a stingle joystick on our Xbox controller. This is not the configuration we use for competitions, but is simpler to teach.

Lets add some code to the Operator Interface file (`src/main/java/frc/robot/OI.java`). This file is where we define every human input.
```java
package frc.robot;

import edu.wpi.first.wpilibj.XboxController;
import edu.wpi.first.wpilibj.GenericHID;

public class OI {
    // Note, I have removed all of the comments for this example. Feel free to leave them in your code. They are helpful.

    public XboxController m_driverController = new XboxController(0);

    public double getThrottle(){
        return m_driverController.getY(GenericHID.Hand.kLeft) * -1;
    }

    public double getTurn(){
      return m_driverController.getX(GenericHID.Hand.kLeft);
    }
}
```

We start off with out imports.
```java
import edu.wpi.first.wpilibj.XboxController;
import edu.wpi.first.wpilibj.GenericHID;
```
These simply tell the JVM that we will be using the `XboxController` and `GenericHID` helper classes from WPIlib.

We need to specify which controller we are reading from (we usually have more than one controller plugged in at a time).
```java
public XboxController m_driverController = new XboxController(0);
```
In this case, we are reading from controller `0`.

Next, we define our `getThrottle` method.
```java
public double getThrottle(){
    return m_driverController.getY(GenericHID.Hand.kLeft) * -1;
}
```
This method will read data from the driver's Xbox controller and return it. Notice the `* -1`? That is required when reading from the **Y** axis of a joystick.

Now, we do the same for `getTurn`, except we are reading from the **X** axis this time, and do not need to invert the value.
```java
public double getTurn(){
    return m_driverController.getX(GenericHID.Hand.kLeft);
}
```
That is it for reading user inputs. Now, on to controlling motors.

## Controlling motors
In order to move the robot's wheels, we need to control their motors. This can be done with a [Subsystem]({{site.baseurl}}/docs/guides/command-base#subsystems).

Create a new file called `DriveTrain.java` in the `src/main/java/frc/robot/subsystems` folder, and add the following template code.
```java
package frc.robot.subsystems;

import com.ctre.phoenix.motorcontrol.can.WPI_TalonSRX;

import edu.wpi.first.wpilibj.command.Subsystem;
import edu.wpi.first.wpilibj.drive.DifferentialDrive;

public class DriveTrain extends Subsystem {

    WPI_TalonSRX left;
    WPI_TalonSRX right;
    DifferentialDrive drive;

    public DriveTrain() {

    }

    @Override
    protected void initDefaultCommand() {
        
    }

}
```

You will also need to add the CTRE vendordep. Feel free to ignore this step until you want to test the code. At that point, ask a returning team member for help.

The code you have added is just a template, and follows the same style as the Operator Interface. Next, we need to add two motors and link them together. Add the following to the `DriveTrain` method:
```java
left = new WPI_TalonSRX(1);
right = new WPI_TalonSRX(2);

drive = new DifferentialDrive(left, right);
drive.setSafetyEnabled(false);
```

The first two lines set up two motors, with IDs `1` and `3`. These numbers are used by the RoboRIO to identify which motor to control. The last two lines link the two motors together into a wrapper class that we have assigned to the variable `drive`.

Now, we simply need a method to turn joystick data into motor commands:
```java
public void arcadeDrive(double speed, double rotation) {
    drive.arcadeDrive(speed, rotation);
}
```

This passes `speed` and `rotation` to `drive`'s `arcadeDrive` method.

## Feeding joystick data to the DriveTrain
WIP