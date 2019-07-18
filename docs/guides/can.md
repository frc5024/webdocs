---
layout: default
title: "Configuring the CAN network"
parent: "Guides"
permalink: /docs/guides/can-config
---

# Configuring the CAN network
This guide is adapted from the [Toronto Coding Collective](https://www.torontocodingcollective.com)

The CAN bus tools supplied by CTRE can be used to update the CAN Bus device Firmware. This tool is required to update the firmware on the Power Distribution Panel (PDP) and Pneumatics Control Module (PCM) and to update any CAN based Victor or Talon speed controllers.

To install the CAN bus tools:

 - Download and install the CTRE Phoenix Framework Installer from the link below. Ignore the fact that it is on the Hero Development Board page, this is the correct tool!
 - Connect to the RoboRIO using a USB Cable (do not use an Ethernet connection)
 - Start the Phoenix Tuner (not the LifeBoat)!
 - Click 'Install Phoenix Library/Diagnostics' button to download the tools to the RoboRio
 - Use the CAN Devices tab to view and update CTRE connected CAN devices. 

[Download](http://www.ctr-electronics.com/hro.html#product_tabs_technical_resources){: .btn }