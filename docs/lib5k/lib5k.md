---
layout: default
title: Lib5K
nav_order: 4
has_children: true
permalink: /docs/lib5k
authors: ['ewpratten']
---

# Lib5K-core & Extensions

Lib5K is 5024's robotics library, and has been in use since the 2019 offseason. This library is built around a system of modules (we call them extensions). This allows you to pick and choose which parts of the library you need for your project, and makes refactoring much easier.

## Extensions

All Lib5K extensions rely on the core library called [Lib5K-core](https://github.com/frc5024/lib5k-core/tree/master). To get started with extensions, your project must be set up to use Lib5K-core. 

### Setting up Lib5K-core

To set up the core, open your project's `build.gradle` file, and add the following line to your project's `repositories` block. If there is none, make one with `repositories{}`.

```groovy
// Add Jitpack maven source
maven { setUrl("https://jitpack.io") }
```

Next, declare the dependency in your project's `dependencies` block with:

```groovy
// Lib5K-core
implementation 'com.github.frc5024:lib5k-core:master-SNAPSHOT'

// All Lib5K extensions should be declared here by pasting in the "implementation" line from webdocs
// ...
```

### Available extensions

The following extensions are available for use, and can be installed by adding their respective implementation declarations to your project's `build.gradle` file.

 - AsyncHAL ([GitHub](https://github.com/frc5024/AsyncHAL)) ([Webdocs](https://cs.5024.ca/webdocs/docs/libraries/asynchal))
   - Adds callback support to common sensors
   - `implementation 'com.github.frc5024:asynchal:master-SNAPSHOT'`
 - PurePursuit ([GitHub](https://github.com/frc5024/PurePursuit))
   - Adds a [Pure Pursuit](https://www.ri.cmu.edu/pub_files/pub3/coulter_r_craig_1992_1/coulter_r_craig_1992_1.pdf) controller, and path generation tools
   - `implementation 'com.github.frc5024:purepursuit:master-SNAPSHOT`