---
layout: default
title: AsyncHAL
nav_order: 0
has_children: true
parent: "Our Libraries"
permalink: /docs/libraries/asynchal
authors: ['ewpratten']
---

# AsyncHAL

AsyncHAL is a java library designed to provide a [callback interface](https://en.wikipedia.org/wiki/Callback_(computer_programming)) for devices connected to the RoboRIO. This works by running a thread at 100hz that checks for new data from all sensors. If new data is found, the associated callback method is run.