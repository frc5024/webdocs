# Reading Data From an Xbox Controller
We use Xbox controllers  to control our robots. This page explains how to interact with a controller from the robot code.

This tutorial assumes that there is an `XboxController` object called `controller`. In our code, we usually name our controllers `driver_controller` and `operator_controller`.

## Reading a Button Press
WPIlib exposes three main methods for reading a button press. These follow the following format:
```Java
controller.get<Name>Button<Action>();
```

For example, to check if the **A** button has been released, the following method should be used:
```Java
controller.getAButtonReleased();
```

To check if the **X** button has been pressed, the following method should be used:
```Java
controller.getXButtonPressed());
```

Finally to check the current state of the **B** button, the following method should be used:
```Java
controller.getBButton();
```

## Reading Joystick Data
Both an **X** and **Y** axis can be read from both joysticks on an Xbox controller. These re done throught the following methods. To specify which joystick to read from, change the `Hand` argument.
```Java
// Read the left joystick's X axis
controller.getX(GenericHID.Hand.kLeftHand);

// Read the right joystick's Y axis
controller.getY(GenericHID.Hand.kRightHand);
```

## Reading Data From the Triggers
The triggers are quite similar to the joysticks, and can be accessed with the following methods:
```Java
// Left hand
controller.getTriggerAxis(GenericHID.Hand.kLeftHand);

// Right hand
controller.getTriggerAxis(GenericHID.Hand.kRightHand);
```

## Reading a Bumper Press
Similarly to a joystick or trigger, you must specify which hand to use when reading a bumper.
```Java
// Left hand
controller.getBumper(GenericHID.Hand.kLeftHand);

// Right hand
controller.getBumper(GenericHID.Hand.kRightHand);
```