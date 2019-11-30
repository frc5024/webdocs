---
layout: default
title: "RoboRIO"
parent: "Learning"
permalink: /docs/learn/roborio
authors: ["ewpratten"]
---

# RoboRIO Documentation

![RoboRIO]

The [RoboRIO](https://www.ni.com/en-ca/support/model.roborio.html) is an industrial robotics controller built by [National Instruments](http://www.ni.com/en-ca.html), and contracted by FIRST for use by FRC teams from 2015 to 2021.

## Hardware

![RoboRIO without cover]

The RoboRIO is based on a [Xilinx Zynq-7020](https://www.xilinx.com/products/silicon-devices/soc/zynq-7000.html) SoC. This chip both contains an [ARM Cortex-A9](https://en.wikipedia.org/wiki/ARM_Cortex-A9) CPU, and an FPGA.


### Specifications
The RoboRIO has a dual core ARM Cortex-A9 processor, running with a clock speed of 667mhz. The RIO also has 512 MB of on-board storage, and 256 MB of RAM, clocked at 533mhz.

A full overview of the the RoboRIO I/O and device info can be found on the [RoboRIO Specification sheet](https://www.ni.com/pdf/manuals/375275a.pdf).

<!-- TODO: Add FPGA info -->
<!-- ### The FPGA
{WIP} -->

## Software
The RoboRIO runs a Linux + [Busybox](https://busybox.net/) OS with [realtime extensions](https://en.wikipedia.org/wiki/RTLinux) for interaction with the FPGA. This OS also comes with it's own package manager, [OPKG](https://en.wikipedia.org/wiki/Opkg), which can be used to install additional tools onto the RIO (Like GCC, or Python).

The OS, by default, has two notable users. `admin`, the system administrator, and `lvuser`. `lvuser` is the user that runs all software on the RoboRIO. Upon startup, the [Bash](https://en.wikipedia.org/wiki/Bash_(Unix_shell)) script located at `/home/lvuser/robotProgram` is executed by the `lvuser` user, and the contents of this script should run the main user program.

By default, the RIO will only run [LabVIEW](https://en.wikipedia.org/wiki/LabVIEW) or native programs. Other languages and tools can be installed and configured by the user. To run Java software, tools like [GradleRIO](https://github.com/wpilibsuite/GradleRIO) will load a custom [JVM](https://en.wikipedia.org/wiki/Java_virtual_machine) onto the RIO. Some FRC teams choose to develop with [ROS](https://en.wikipedia.org/wiki/Robot_Operating_System), and can use tools to deploy an ROS environment to their RoboRIO.

### Hardware Access Layer
National Instruments provides a Hardware Access Layer (HAL) library for interacting with the FPGA. The HAL contains hooks for the following:
 - I/O
   - PWM
   - DIO
   - AIO
   - Relays
 - Networking
   - CAN
   - FRCNetConn
     - DriverStation
     - [Usage Reporting](https://frcture.readthedocs.io/en/latest/driverstation/usage_reporting.html)

### Software libraries
Multiple software libraries exist for interacting with the RoboRIO FPGA:
 - [NI C library](http://www.ni.com/download/labview-roborio-toolkit-2015/5558/en/)
 - [NI C++ Library](https://github.com/wpilibsuite/ni-libraries)
 - [WPILib](https://github.com/wpilibsuite/allwpilib/)
 - [RobotPY](https://robotpy.readthedocs.io/en/stable/)
 - [RobotDotNet](https://github.com/robotdotnet)
 - [First Rust Competition](https://github.com/first-rust-competition)
 - [Emojicode FRC](https://gitlab.com/Redrield/affront-to-god/)

#### Extension libraries
Many libraries also exist to extend the functionality of the libraries listed above. For example:
 - [Lib5K](https://github.com/frc5024/lib5k)
 - [MeanLib](https://github.com/TeamMeanMachine/meanlib)
 - [CurtinFRC Library](https://github.com/CurtinFRC/Common)

[RoboRIO]: /webdocs/assets/img/roborio.jpg
{:width="250px"}

[RoboRIO without cover]: /webdocs/assets/img/roborio-uncovered.jpeg
{:width="250px"}