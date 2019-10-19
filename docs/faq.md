---
layout: default
title: "FAQ"
nav_order: 14
permalink: /docs/faq
authors: ['ewpratten']
---

# Frequently Asked Questions

## Why do I get build errors from the Compressor subsystem?
This is due to a namespacing issue. We generally try to use other names that mean the same thing. In the past, the names: `cCompressor`, `Pressurizer`, and `Pneumatics` were used to fix this problem. Not enough information has been gathered yet to file a bug report upstream with the WPIlib team.

## Gradle is throwing "class not found" errors
This is a common issue on Linux systems due to versioning issues. Generally, the best solution is to:
 - Uninstall Gradle from the system
 - Install the latest Gradle package from [their website](https://gradle.org/install/) NOT your package manager
 - Run `gradle wrapper` in the project folder

## Motors are behiving unexpectadly
There is a high chance that this is due to motor safety being enabled. To fix this, call the `.setSafetyEnabled(false)` method on all SpeedController, and DifferentialDrive objects related to, or using that motor.