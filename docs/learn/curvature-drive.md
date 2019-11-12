---
layout: default
title: "Curvature Drive"
parent: "Learning"
permalink: /docs/learn/curv
authors: ['hyperliskdev']
---

# Curvature Drive

Curvature drive is a method inside of the DifferentialDrive class in WPILib 

## What does Curvature Drive do?

Curvature drive is a type of drive just like Arcade or Tank drive. Curvature drive is different in a few key ways;

- isQuickTurn method is used to quickturn on the stop, as it is default off.
- Turning speed withput isQuickTurn == true, is based on how fast the robot is moving.

