---
layout: default
title: "OpenMesh Configuration"
parent: "Guides"
permalink: /docs/guides/openmesh
authors: ['ewpratten']
---

# Configuring an OpenMesh Router

Also refered to as "Flashing a radio", the routers we use on our robots (models: om5p-an and om5p-ac) must run a custom linux-based image provided by FIRST. This guide is a slightly modified version of [118's pac-bot guide](https://ccisdrobonauts.org/uploads/12/8f/128f1b30391ad7a196606e2b57a1a6b1.pdf).

## Flashing
Be patient when configuring the Open Mesh radios, it takes about 30seconds for them to boot. Watch the lights, they will come on, flash for a little while, then theyall go off and it starts over. Don’t start configuring until the network light starts blinking ​thesecond time.

The Radio Flashing Utility provides many options for various routers. These are the three configurations that we commonly use:

### Demonstrations and in the shop

In most cases, you will want the driver's laptop to connect directly to your robot, so the radio on your robot will need to be configured as an access point. Due to the age of our laptops, we always use the 2.4GHZ band for our network.

![Screenshot of the Radio configuration Utility](/webdocs/assets/img/radioconfig.png)

After connecting directly to the radio via ethernet and waiting for the radio to power on,

 1. Enter your team number
 2. Enter `raiderrobotics` as the password
 3. Select `OpenMesh`
 4. Choose `2.4GHZ`
 5. If this radio is being used at any time throuought the season (January to April) Both `BW Limit` and `Firewall` **MUST** be enabled. If this radio is being configured for offseason use only, disable these options.
 6. Click on the Configure button and follow the on screen instructions. (If the radioconfiguration fails, a common fix is to temporarily disable any other network interfaces, such as wifi, that you might have running)

### At a competition

At each competition, you will need to use the Radio Configuration Kiosk set-up by the event at pit admin. Try to get this done as early as possible, so the team can proceed with system checks in the pit. When running in this mode, the Radio Configuration Utility will configure each team’s radio to act as a bridge with a unique SSID and password that team and competition.

### At offseason events

During our offseason events and demonstrations that involve many robots in a small space, using a central router for everyone is a great way to reduce interference, and extend the range of every robot.

![Offseason radio configuration](/webdocs/assets/img/fieldradio.png)

After connecting your laptop directly to the radio and waiting for the radio to power on,

 1. Enter your team number
 2. From the Tools Menu, select FMS Offseason Mode
 3. Enter The ssid of the field router. If the event is using ThriftyField, use `ThriftyField` as the SSID.
 4. The password should be the same as the field network, or blank.
 5. Select `OpenMesh`
 6.  Both `BW Limit` and `Firewall` should be disables for optimal latency
 7. Click on the Configure button and follow the on screen instructions.