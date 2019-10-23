---
layout: default
title: "Your First Program"
parent: "Learning"
permalink: /docs/learn/your-first-program
authors: ['ewpratten', 'exvacuum', 'slownie']
---

# Writing your first robot program
This lesson assumes that you have already installed the FRC [development tools]({{site.baseurl}}/docs/guides/installing-tools) on your computer, or you are using a computer provided by the team. 

Open Visual Studio Code, and follow [WPIlib's instructions](https://frc-docs.readthedocs.io/en/latest/docs/software/wpilib-overview/creating-robot-program.html#creating-a-new-wpilib-project) for starting a new project. Choose 'Template' when selecting a project type. Make sure to set the team number to `5024`, Java as your programming language, and `Command Robot` 

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
Firstly, we should start off with some controls. Our drive team uses Xbox controllers to drive our robots, so we will be writing some code for one of these controllers. To drive our bot, we will be using just a stingle joystick on our Xbox controller. This is not the configuration we use for competitions, but it is simpler to teach.

Let's add some code to the Operator Interface (OI) file (`src/main/java/frc/robot/OI.java`). This file is where we define every human input.
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

Let's start off with out imports.
```java
import edu.wpi.first.wpilibj.XboxController;
import edu.wpi.first.wpilibj.GenericHID;
```
These imports simply tell the JVM that we will be using the `XboxController` and `GenericHID` helper classes from WPIlib.

We need to specify which controller we are reading from (we usually have more than one controller plugged in at a time).
```java
public XboxController m_driverController = new XboxController(0);
```
In this case, we are reading from controller `0` (The driver's controller).

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

You will also need to add the [CTRE vendordep](http://devsite.ctr-electronics.com/maven/release/com/ctre/phoenix/Phoenix-latest.json). To do this, open the command palette using ctrl+shift+P and search "vendor", select "Manage Vendor Libraries", then "Install New Library (Online)", and paste the previous link. See the [vendor dependencies]({{site.baseurl}}/docs/vendordeps) page for more information. Feel free to ignore this step until you want to test the code. At that point, ask a returning team member for help.

The code you have added is just a template, and follows the same style as the Operator Interface. Next, we need to add two motors and link them together. Add the following to the `DriveTrain` method:
```java
left = new WPI_TalonSRX(1);
right = new WPI_TalonSRX(3);

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
We now need to read the joystick data, and push it to the DriveTrain. This can be done with a [Command]({{site.baseurl}}/docs/guides/command-base#commands).

Create a new file called `DriveControl.java` in the `src/main/java/frc/robot/commands` folder, and add the following template code.
```java
package frc.robot.commands;

import edu.wpi.first.wpilibj.command.Command;
import frc.robot.Robot;

public class DriveControl extends Command {

	@Override
	protected void execute() {
        
	}

	@Override
	protected boolean isFinished() {
		return false;
	}

}
```

This is a basic command class. As long as `isFinished` returns `false`, the `execute` method will be called once every 20ms by the robot. We can use this to our advantage by writing some code to read our joystick data here.

Inside the `execute` method, add these two lines. They will call the `getThrottle` and `getTurn` methods we made in the first section, and store the data.
```java
double speed = Robot.m_oi.getThrottle();
double rotation = Robot.m_oi.getTurn();
```

Now, we just need to pass this data to the subsystem we just made. This can be done with the following line. It will call the `arcadeDrive` method we just made, and give it our speed and rotation valuse.
```java
Robot.m_driveTrain.arcadeDrive(speed, rotation);
```

## Adding the subsystem to the robot
That's almost everything! We just need to write a few lines of code to tie everything together.

In the `src/main/java/frc/robot/Robot.java` file, we need to add the following to the list of imports in order to import our new Command and Subsystem:
```java
import frc.robot.commands.DriveControl;
import frc.robot.subsystems.DriveTrain;
```

Next, we need to tell the robot that we made a subsystem and command. Add the following under the line that says `public static OI m_oi;`:
```java
public static DriveTrain m_driveTrain;

DriveControl m_driveControl;
```

Next, we need to create the two objects
```java
m_driveControl = new DriveControl();
m_driveTrain = new DriveTrain();
```

These go under the `m_oi = new OI();` line.

Finally, add the following code to the `teleopInit()` method we created earlier in the `Robot` class:
```java
if (m_driveControl != null){
    m_driveControl.start();
}
```

This code checks that `m_driveControl` has not started, and then starts it. Without this, the code we have written will not work.

## Conclusion
That's it! You now have your first piece of robot code (and it can actually drive!).

This guide was not designed to teach you how to program, but to show you around the general file structure of our robot code, and where each type of code goes. Feel free to come talk to a returning mentor, or team lead to see what you can add to your code next.