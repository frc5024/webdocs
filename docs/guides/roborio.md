# Flashing a RoboRIO

This guide is based off of [118's pac-bot guide](https://ccisdrobonauts.org/uploads/12/8f/128f1b30391ad7a196606e2b57a1a6b1.pdf).

The RoboRIO is a computer designed for use on robots. It has several Reconfigurable Input andOutput (RIO) ports and several communication ports. The RoboRIO runs a customized real-time Linux operating system. Updates to the operating system are released as image files that can be installed using the RoboRIO Imaging tool (or NI MAX). The imaging tool can also be used to set a team number on the RoboRIO.

## The imaging process

To image a RoboRIO, you should connect to the RoboRIO with a USB cable plugged into the RoboRIO USB device (USB-B) port. It is safest to disconnect your laptop from all other networks (including wireless networks) when imaging a RoboRIO. After connected, make sure the RoboRIO is powered on, and start the RoboRIO Imaging tool. It should automatically scan and locate your RoboRIO. If not, you can click on the rescan button. When your RoboRIO is found:

 1. Make sure the RoboRIO is selected
 2. Enter `5024` as the team number
 3. Enable `Console Out`
 4. Disable `Disable RT`
 5. Enable `Format Target`
 6. Select the desired (latest) image
 7. Click Reformat to begin the imaging process

A full walkthrough of this process can be found [HERE](https://wpilib.screenstepslive.com/s/4485/m/13503/l/144984-imaging-your-roborio)

