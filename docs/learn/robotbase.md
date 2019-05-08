# The Various Robot Bases
All good robot programs start with a good base. This is called the RobotBase.

WPIlib provides these three solid bases to choose from when programming your robot:
 - Iterative
 - Timed
 - Command-Based

## The Iterative Robot
The IterativeRobot base class has **methods that are periodically called each time new data arrives from the Driver Station**. The idea is that for each mode that the robot is operating in (autonomous, teleop, or test) the appropriate periodic method is called where the program does a small amount of work. **It is important not to have any long running code in the periodic methods such as loops or delays. Doing so could result in missing driver station updates that can negatively impact robot performance**. Each period is approximately 20 milliseconds by can vary depending on CPU load on the roboRIO, the driver station laptop, or network traffic. If you require precise timing, for example to implement robot control algorithms it is not recommended and you should instead use TimedRobot (below) which has precise timing between periods.

## The Timed Robot
TimedRobot is the same as IterativeRobot except that it **uses a timer (Notifier) to guarantee that the periodic methods are called at a predictable time interval**. When getting driver station data such as joystick values the most recent value will be provided since the time interval may not line up with the 20 millisecond delivery of data. **This is the recommended base class for most robot programs**. Just as with IterativeRobot, **it is very important to not have long running code or loops in the periodic methods or the timing may slip**.

## The Command-based Robot
While based on the TimedRobot base class, **the command based robot programming style is recommended for most teams**. It makes it easy to break up the program into Commands which each implement some robot behavior such as raising an arm to some position, driving for some distance, etc. It also makes the program easily extensible and testable. The RobotBuilder utility (included with the eclipse plugins) provides an easy way of organizing the program. The dashboards (SmartDashboard and Shuffleboard) allow you to easily debug and test command based programs.

## The MagicBot Robot
This final robot base is specifically designed for use with the Python programming language. Due to the fact that this framework only exsists in the Python library, we will not cover it in this guide.

If you would like to read more about the MagicBot framework, take a look at the [robotpy docs](https://robotpy.readthedocs.io/en/stable/frameworks/magicbot.html)

## What Do We Use?
We currently use the Command-based framework for all of our code. This is also the framework that will be covered fully in this guide.

We use the Command-based framework because it clearly seperates the various functions of the robot, and forces the team to write effective, and clean code.