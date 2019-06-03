# Example robot log

We like logs. A lot. Here are some example logs from various situations.

## Robot Boot

```
********** Robot program starting **********
Robot starting...
Welcome 5024!
Current time: 0.0346
ROBOT: Starting CameraServer
CS: USB Camera 0: Connecting to USB camera on /dev/video0
CS: USB Camera 0: set format 1 res 320x180
CS: USB Camera 0: Connecting to USB camera on /dev/video0
CS: USB Camera 0: set format 1 res 320x240
CS: USB Camera 0: set FPS to 15
Main Camera initialized on TCP port 1184
ROBOT: Constructing Subsystems
ROBOT: [DriveTrain] Constructing GearBoxes out of motor pairs
NT: server: client CONNECTED: 127.0.0.1 port 36058
ROBOT: [DriveTrain] Limiting current on both gearboxes. Peak: 35A, Hold: 33A, Timeout: 33ms
ROBOT: [DriveTrain] Drivebase has been set to: Unsafe
ROBOT: [DriveTrain] Loading gyro for drivetrain
ROBOT: [DriveTrain] Gyro has been reset to: 0.0
ROBOT: [Ledring] Constructing "solenoid" for led control
ROBOT: [Slider] Constructing WPI_TalonSRX for slider
ROBOT: [Slider] Constructing Hall effect sensors for slider
ROBOT: [Slider] Configuring PID for slider
ROBOT: [Slider] Set PID gains to: 1.0P, 0.0I, 0.0D
ROBOT: [Finger] Constructing solenoid
ROBOT: [Piston] Constructing solenoid
ROBOT: [Compressor] Constructing Compressor class
ROBOT: [Flap] Constructing solenoid
ROBOT: Initializing Subsystems
ROBOT: Constructing Superstructure
ROBOT: [Vision] Starting monitor thread
ROBOT: Constructing Commands
ROBOT: Setting up Notifiers
ROBOT: FieldStatusThread Starting
ROBOT: [ConnectionMonitor] Started monitoring driverstation connection
ROBOT: Starting vision thread
ROBOT: Setting NetworkTables period time to: 0.01
LIBRARY: Main Camera's connection mode has been set to: Stay Awake
INFO: [DriveTrain] NeutralMode has been set to: Brake
ROBOT: Robot Disabled
Current time: 0.0346
INFO: [DriveTrain] NeutralMode has been set to: Coast
ROBOT: [ConnectionMonitor] The robot has lost connection!
INFO: [Ledring] Wanted state set to: kStrobe
```

## CAN errors due to running in simulation mode instead of on a RoboRIO

This is perfectly normal to see. It can be ignored while running a simulation.

```
CTR: CAN frame not received/too-stale.
        Talon SRX 1 GetSelectedSensorPosition
CTR: CAN frame not received/too-stale.
        Talon SRX 1 GetSelectedSensorPosition
CTR: CAN frame not received/too-stale.
        Talon SRX 3 GetSelectedSensorPosition
CTR: CAN frame not received/too-stale.
        Talon SRX 3 GetSelectedSensorPosition
CTR: Firm Vers could not be retrieved. Use Phoenix Tuner to check ID and firmware(CRF) version. 
        Talon SRX 6
```