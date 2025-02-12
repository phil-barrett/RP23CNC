# RP23CNC
RP235x based breakout board for grblHAL.

## Status
Received first build of the board (2/10/2025). First test results: It boots and loads grblHAL firmware. All inputs and outputs work. 12V isolated inputs work.  Prox sensors work. Step, Direction and Enable for all 5 axes work. Ethernet (via the Wiznet module) works. Long job runs completed sucessfully. 5V regulator runs hot. Coming up: UART and I2C testing as well as more long job tests.

Key changes planned or considered.  
* The linear power supply for 12V to 5V needs to be changed. With the Ethernet adaptor, it runs at about 1W of dissipation which pushes the temperature to around 80C over ambient temperature. While this is still within the regulator's spec for most cases, the plan is to replace it with an SMPS.  The V 0.92 board is usable with Ethernet by using VUSB to feed 5V the 3.3V regulator.
* V 0.92 uses the RasPi specified crystal and inductor (for the 1.1V) supply.  These are surprisingly expensive components that add a fair amount of cost to the final price so the plan is to move to using less expensive parts.
* Spacing of screw terminal increased by 0.08mm to allow easier assembly.
* SD Card adaptor moved to allow more relaible depanelling.
* Consider moving to a surface mount trimmer potentiometer to decrease cost (BOM and assembly).
* Consider Making digital inputs 5V tolerant. (RP2350 inputs are 5V tolerant when powered at 3.3V, but not when the chip is unpowered.)
* One GPIO is available. Not sure what to use it for - digital input, digital output, ? Suggestions welcome.

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
  * 3.3V output 
- MicroSD Card support
- Ethernet Support via optional WizNet module
