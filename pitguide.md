# Programming Pit Guide
This document contains the answers to common questions asked by judges and other teams in the pits.

## Q&A

### What programming language does the team use?
We use **both C++ and Python**. Any code that directly inferfaces with the hardware or sensors is in C++, everything else, including our vision and logging systems, are written in Python (3.7 to be exact)

### What robot base / type do we use?
We mainly use WPIlib's *Command Based* structure, but some of our components have moved to our own *Stack Based* structure.

### Do we use GIT?
YES! Feel free to view and contribute to our code at [github.com/frc5024](https://github.com/frc5024)

### What camera do we use / Do we use a limelight?
No. We do not use a limelight, we use a **Microsoft lifecam 3000**

### What coprocessor do we use?
We use a **raspberry pi 3B+** rinning WPIlib's vision image.

### How do we network everything together?
We have a gigabit ethernet switch mounted on the robot. This allows for the Pi and RIO to communicate with eachother and the radio.

### What is the most unique part of our code?
(This will be the preferred answer once we are fully operational with our motion code.)

During sandstorm, we make use of motion profiling / motion control to help us achive a fast second hatch placement. This is done by motion profiling from the cargo ship to the area infront of the loading station. To correct for any possible driver error, we then find our relitive location from the load-in port via our vision system. This feeds data into a secondary, real-time generated, motion profiling system that brings us in the rest of the way to the hatch waiting for us.

(The following answer is how we won Innovation in Control at Ryerson.)

We make use of an array of hal effect sensors, mounted on our robot's slider, to constantly keep track of the slider's position. This allows us to automatically home / recentre the slider during match play after a hatch has been placed. This way, the drivers allways know that the slider is in the same position when they need to use it again.

