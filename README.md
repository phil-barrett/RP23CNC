# RP23CNC
RP235x based breakout board for grblHAL.

## Status
Received first build of the board today (2/10/2025).  Briefly tested.  It boots and loads grblHAL firmware. Will be testing all features in the next few days.  Beta testers should expect to have their boards mailed within a week.

Bad photo (better ones coming when I get some time).

![V0.92 build](https://github.com/phil-barrett/RP23CNC/blob/main/Photos/T2100316.JPG)

## Model Rendering
![RP2350B based RP23CNC](https://github.com/phil-barrett/RP23CNC/blob/main/RP23CNC.png)

## Features
- 5 Axis
  * Step, Direction, Enable outputs, 5V compatible
  * Limit Input with LED, 12V compatible
  * Servo Error Input with LED, 12V compatible
- Standard Grbl inputs, 12V compatible
  * Cycle Start, Feed Hold, Halt, Safety Door, Probe
- Isolated input section
  * 12V compatible
  * Joinable to main 12V section
- Digital Outputs
  * Flood, Mist, Aux 0, Aux 1, Aux 2, Dust Collector
- Relay Coil Outputs
  * 5V or 12V selectable, Capable of driving 100 mA coils
  * Flood, Mist, Aux 0, Aux 1, Aux 2, Dust Collector, Spindle Enable
- Digital Inputs
  * 3.3V compatible
  * D0, D1, D2
 - Spindle Support
   * PWM, 0-10V, 0-5V support
   * Enable, Direction, PWM,  5V compatible.
- 2 UARTs
- Power Section
  * 12V Main board input
  * 12V Isolated input (joinable to Main 12V)
  * 5V output
- MicroSD Card support
- Ethernet Support via optional WizNet module
