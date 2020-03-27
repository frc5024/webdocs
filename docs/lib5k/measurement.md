---
layout: default
title: "Measurement"
parent: "Lib5K"
permalink: /docs/lib5k/measurement
authors: ['exvacuum']
---

# Measurement
The unified measurement conversion utility is a simple and useful tool for converting between units of measurement. Supporting conversions between most commonly-used units of measurement, this tool is designed to save you the time it takes to Google "mm to in", as well as improving readability for others when they review your code.

## Usage Instructions
The Measurement class contains a single static method:
```java
public static double convert(double value, double units_from, double units_to){
        //Convert to mm, then to desired output
        return (value * units_from)/units_to;
}
```

The first argument of this method, `value`, is simply the vlaue of the measurement without units. The next two arguments, `units-from` and `units_to`, accept static constants defiined within the class. The currently supported units are as follows:
```java
Measurement.MM;
Measurement.CM;
Measurement.M;
Measurement.IN;
Measurement.FT;
Measurement.YD;
```

In essence, the conversion method converts `value`, in `units_from`, into millimeters, and then from millimeters into the desired `units_to`.

## Example Usage

```java
System.out.println(Measurement.convert(200, Measurement.CM, Measurement.M)); //Prints "2"

//OR if used with a static import
System.out.println(convert(200, CM, M)); //Prints "2", looks nicer.
```