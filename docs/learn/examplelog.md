---
layout: default
title: "Logfile Examples"
parent: "Learning"
permalink: /docs/learn/example-logs
authors: ['ewpratten']
---

# Example robot log

We like logs. A lot. Here are some example logs from various situations.

## Robot Boot

```
INFO at 0.36s: io.github.frc5024.lib5k.examples.autonomous_path_following.Main::<init>() -> Adding autonomous paths
INFO at 0.38s: io.github.frc5024.lib5k.autonomous.RobotProgram::addAutonomous() -> Added autonomous sequence: ForwardOneMeter
INFO at 0.38s: io.github.frc5024.lib5k.hardware.ni.roborio.FaultReporter::handleRailStatuses() -> 3v3 Rail Enabled
DEBUG at 0.87s: io.github.frc5024.common_drive.DriveTrainBase::runIteration() -> DriveTrain.periodic() has not yet been run by the scheduler... waiting
INFO at 0.87s: io.github.frc5024.lib5k.logging.USBLogger::update() -> A CMOD occured
DEBUG at 0.89s: io.github.frc5024.common_drive.DriveTrainBase::runIteration() -> DriveTrain.periodic() has not yet been run by the scheduler... waiting
DEBUG at 0.91s: io.github.frc5024.common_drive.DriveTrainBase::runIteration() -> DriveTrain.periodic() has not yet been run by the scheduler... waiting
DEBUG at 0.93s: io.github.frc5024.common_drive.DriveTrainBase::runIteration() -> DriveTrain.periodic() has not yet been run by the scheduler... waiting
DEBUG at 0.95s: io.github.frc5024.common_drive.DriveTrainBase::runIteration() -> DriveTrain.periodic() has not yet been run by the scheduler... waiting
DEBUG at 0.97s: io.github.frc5024.common_drive.DriveTrainBase::runIteration() -> DriveTrain.periodic() has not yet been run by the scheduler... waiting
DEBUG at 0.99s: io.github.frc5024.common_drive.DriveTrainBase::runIteration() -> DriveTrain.periodic() has not yet been run by the scheduler... waiting
DEBUG at 1.01s: io.github.frc5024.common_drive.DriveTrainBase::runIteration() -> DriveTrain.periodic() has not yet been run by the scheduler... waiting
DEBUG at 1.03s: io.github.frc5024.common_drive.DriveTrainBase::runIteration() -> DriveTrain.periodic() has not yet been run by the scheduler... waiting
DEBUG at 1.05s: io.github.frc5024.common_drive.DriveTrainBase::runIteration() -> DriveTrain.periodic() has not yet been run by the scheduler... waiting
DEBUG at 1.07s: io.github.frc5024.common_drive.DriveTrainBase::runIteration() -> DriveTrain.periodic() has not yet been run by the scheduler... waiting
DEBUG at 1.09s: io.github.frc5024.common_drive.DriveTrainBase::runIteration() -> DriveTrain.periodic() has not yet been run by the scheduler... waiting
DEBUG at 1.10s: io.github.frc5024.common_drive.DriveTrainBase::runIteration() -> DriveTrain.periodic() has not yet been run by the scheduler... waiting
DEBUG at 1.13s: io.github.frc5024.common_drive.DriveTrainBase::runIteration() -> DriveTrain.periodic() has not yet been run by the scheduler... waiting
DEBUG at 1.13s: io.github.frc5024.common_drive.DriveTrainBase::runIteration() -> DriveTrain.periodic() has not yet been run by the scheduler... waiting
DEBUG at 1.15s: io.github.frc5024.common_drive.DriveTrainBase::runIteration() -> DriveTrain.periodic() has not yet been run by the scheduler... waiting
INFO at 1.16s: io.github.frc5024.lib5k.autonomous.RobotProgram::disabledInit() -> Robot disabled
INFO at 1.17s: io.github.frc5024.lib5k.examples.autonomous_path_following.Main::disabled() -> Stopping drivetrain
DEBUG at 1.17s: io.github.frc5024.common_drive.DriveTrainBase::runIteration() -> DriveTrain.periodic() has not yet been run by the scheduler... waiting
INFO at 1.17s: io.github.frc5024.lib5k.examples.autonomous_path_following.Main::disabled() -> Stopping drivetrain
DEBUG at 1.17s: io.github.frc5024.common_drive.DriveTrainBase::runIteration() -> DriveTrain.periodic() has not yet been run by the scheduler... waiting
INFO at 1.17s: io.github.frc5024.common_drive.DriveTrainBase::stop() -> Stopped DriveTrain
DEBUG at 1.18s: io.github.frc5024.common_drive.DriveTrainBase::runIteration() -> DriveTrain.periodic() has not yet been run by the scheduler... waiting
INFO at 1.26s: io.github.frc5024.common_drive.DriveTrainBase::handleOpenLoopControl() -> Switched to open-loop control
INFO at 8.15s: io.github.frc5024.lib5k.autonomous.RobotProgram::autonomousInit() -> Autonomous started
INFO at 8.16s: io.github.frc5024.lib5k.autonomous.RobotProgram::autonomousInit() -> Starting autonomous sequence: ForwardOneMeter
INFO at 8.21s: io.github.frc5024.lib5k.hardware.ni.roborio.FaultReporter::update() -> Robot FPGA outputs have been enabled
INFO at 8.21s: io.github.frc5024.common_drive.DriveTrainBase::setPose() -> Setting pose to: Pose2d(Translation2d(X: 0.00, Y: 0.00), Rotation2d(Rads: 0.00, Deg: 0.00))
INFO at 8.22s: io.github.frc5024.common_drive.commands.PathFollowCommand::initialize() -> Reset path follower
INFO at 8.22s: io.github.frc5024.common_drive.commands.PathFollowCommand::initialize() -> Opening a CSV logfile to save path progress to
INFO at 8.23s: io.github.frc5024.common_drive.DriveTrainBase::setActiveSide() -> Set active side to: kPrimary
INFO at 8.27s: io.github.frc5024.common_drive.DriveTrainBase::handleRabbitChase() -> Switched to 'rabbit chase' mode
INFO at 8.27s: io.github.frc5024.common_drive.DriveTrainBase::handleRabbitChase() -> Position goal is: Translation2d(X: 0.15, Y: 0.00)
INFO at 8.27s: io.github.frc5024.common_drive.DriveTrainBase::handleRabbitChase() -> Switching to default gear
INFO at 9.08s: io.github.frc5024.common_drive.commands.PathFollowCommand::end() -> Robot successfully reached goal pose: Translation2d(X: 1.00, Y: 0.00)
INFO at 9.08s: io.github.frc5024.common_drive.DriveTrainBase::setActiveSide() -> Set active side to: kPrimary
INFO at 9.08s: io.github.frc5024.common_drive.DriveTrainBase::stop() -> Stopped DriveTrain
INFO at 9.08s: io.github.frc5024.common_drive.commands.PathFollowCommand::end() -> Saving CSV logfile
INFO at 9.09s: io.github.frc5024.common_drive.DriveTrainBase::handleOpenLoopControl() -> Switched to open-loop control
INFO at 10.89s: io.github.frc5024.lib5k.autonomous.RobotProgram::disabledInit() -> Robot disabled
INFO at 10.90s: io.github.frc5024.lib5k.examples.autonomous_path_following.Main::disabled() -> Stopping drivetrain
INFO at 10.90s: io.github.frc5024.common_drive.DriveTrainBase::stop() -> Stopped DriveTrain
INFO at 10.93s: io.github.frc5024.lib5k.hardware.ni.roborio.FaultReporter::update() -> Robot FPGA outputs have been disabled
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