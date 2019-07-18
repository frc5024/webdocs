---
layout: default
title: "WPIlib reference"
nav_order: 8
permalink: /docs/wpilib
---

# WPIlib Reference
This guide is adapted from the [Toronto Coding Collective](https://www.torontocodingcollective.com)

## What is WPILib

From the WPILib reference: 

The WPI Robotics library (WPILib) is a set of software classes that interfaces with the hardware and software in your FRC robot’s control system. There are classes to handle sensors, motor speed controllers, the driver station, and a number of other utility functions such as timing and field management. 

## Most Useful WPILib Classes

This is a list of the primary WPILib classes used in robot programming:

### Command Based Programming

 - [Scheduler](https://first.wpi.edu/FRC/roborio/release/docs/java/edu/wpi/first/wpilibj/command/Scheduler.html) - scheduling a command
 - [Command](https://first.wpi.edu/FRC/roborio/release/docs/java/edu/wpi/first/wpilibj/command/Command.html) - the basic framework for all commands
 - [Subsystem](https://first.wpi.edu/FRC/roborio/release/docs/java/edu/wpi/first/wpilibj/command/Subsystem.html) - a container for sensors, motors and pneumatics actuators. Keep in mind that we use our own LoopableSubsystem

### Operator Input (OI) Layer

 - [XboxController](https://first.wpi.edu/FRC/roborio/release/docs/java/edu/wpi/first/wpilibj/XboxController.html) - An interface to the Xbox controllers we use to drive our bots
 - [SendableChooser](https://first.wpi.edu/FRC/roborio/release/docs/java/edu/wpi/first/wpilibj/smartdashboard/SendableChooser.html) - a way to select an auto pattern on the SmartDashboard
 - [SmartDashboard](https://first.wpi.edu/FRC/roborio/release/docs/java/edu/wpi/first/wpilibj/smartdashboard/SendableBuilder.html) - put debug/status information on the SmartDashboard

### Drive Calculator Classes

 - [DifferentialDrive](https://first.wpi.edu/FRC/roborio/release/docs/java/edu/wpi/first/wpilibj/drive/DifferentialDrive.html) - calculator for left/right drive robots
 - [MecanumDrive](https://first.wpi.edu/FRC/roborio/release/docs/java/edu/wpi/first/wpilibj/drive/MecanumDrive.html) - calculator for 4 wheel mecanum drive robots

### Speed Controllers (Motors)

 - [Jaguar, PWMSpeedController, SD540, Spark, Talon, TalonSRX, Victor, VictorSP](https://first.wpi.edu/FRC/roborio/release/docs/java/edu/wpi/first/wpilibj/SpeedController.html) - a motor connected to a PWM port
 - [TalonSRX](https://www.ctr-electronics.com/downloads/api/java/html/classcom_1_1ctre_1_1phoenix_1_1motorcontrol_1_1can_1_1_talon_s_r_x.html) - a TalonSRX connected to the CAN bus (requires the CTRE [vendordep](/webdocs/docs/vendordeps))

### Sensors

 - [AnalogInput](https://first.wpi.edu/FRC/roborio/release/docs/java/edu/wpi/first/wpilibj/AnalogInput.html) - an analog input (ie. proximity sensor)
 - [DigitalInput](https://first.wpi.edu/FRC/roborio/release/docs/java/edu/wpi/first/wpilibj/DigitalInput.html) - a limit switch or other digital input plugged into a DIO port
 - [Counter](https://first.wpi.edu/FRC/roborio/release/docs/java/edu/wpi/first/wpilibj/Counter.html) - a counter attached to a DIO channel used to count fast DIO pulses

### Pnematics

 - [Solenoid](https://first.wpi.edu/FRC/roborio/release/docs/java/edu/wpi/first/wpilibj/Solenoid.html) - a pneumatic single solenoid 
 - [DoubleSolenoid](https://first.wpi.edu/FRC/roborio/release/docs/java/edu/wpi/first/wpilibj/DoubleSolenoid.html) - a penumatic double solenoid

### Key IP Address Lists

 - roboRIO USB: 172.22.11.2
 - roboRIO mDNS: roboRIO-####-FRC.local (where #### is your team number with no leading zeroes) You should be able to use this address to communicate with the roboRIO over either interface through ping, browser, etc.
 - Robot Radio: 10.TE.AM.1 (where TE.AM is your 4 digit team number with leading zeroes if required)
 - DHCP range: 10.TE.AM.20 to 10.TE.AM.199