---
layout: default
title: "PIDProfile"
parent: "Lib5K"
permalink: /docs/lib5k/pidprofile
authors: ['ewpratten']
---

# PIDProfile
A PIDProfile is a data structure for storing [PID Gains](https://en.wikipedia.org/wiki/PID_controller#Loop_tuning). This allows us to swap between profiles depending on the conditions (for example, we could have a profile for concrete, and a profile for carpet).

## Creating a profile
To create a profile, just pass in the gains. 
```java
// PID
new PIDProfile(p,i,d);

// PI
new PIDProfile(p,i);

// P
new PIDProfile(p);
```

These profiles can be passed into the constructor of a [PID](/docs/lib5k/pid) object.
```java
new PID(new PIDProfile(p,i,d));
```

## Profile auto-generation
PIDProfile can also automatically generate a profile based on the [Zeigler-Nichols](https://en.wikipedia.org/wiki/Ziegler%E2%80%93Nichols_method) tuning method.
```java
// Auto-generated profile with a maximum P of 5, and an oscillation period of 1 second

PIDProfile profile = PIDProfile.autoConfig(5.0,1.0);
```

This will generate the `p`, `i`, and `d` values.

## Profile modification
You may want to auto-generate a profile, but make a slight change to a value. This is where `PIDProfile.modify` comes in to play.

```java
// Same generated profile from above, but we are going to increase the P gain by 1
PIDProfile profile = PIDProfile.autoConfig(5.0,1.0).modify(new PIDProfile(1,0.0,0.0));
```