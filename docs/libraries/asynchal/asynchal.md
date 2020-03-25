---
layout: default
title: AsyncHAL
nav_order: 5
has_children: true
permalink: /docs/libraries/asynchal
authors: ['ewpratten']
---

# AsyncHAL

AsyncHAL is a java library designed by 5024 to provide a [callback interface](https://en.wikipedia.org/wiki/Callback_(computer_programming)) for devices connected to the RoboRIO. This works by running a thread at 100hz that checks for new data from all sensors. If new data is found, the associated callback method is run.

## Runnables & Consumers

All callbacks are handled by Java11's `Runnable` and `Consumer<T>` types. It is *strongly* recommended to have a good understanding of these concepts before using this library. A good tutorial can be found here: [Runnables](https://www.geeksforgeeks.org/runnable-interface-in-java/), [Consumers](https://www.geeksforgeeks.org/java-8-consumer-interface-in-java-with-examples/)