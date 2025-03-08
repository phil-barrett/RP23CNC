# RP23CNC
RP235x based breakout board for grblHAL.

## Mar 7, V0.95 boards back.
Using LDO to generate 1.1V works. Alternate crystal works. 5V generation works pretty well. Testing shows buck converter runs at about 10 C above ambient while running a long term test with LED loads on step signal output. Heat imaging shows no hot spots. Made decision to move to USB-C connector.  
![V0.95](https://github.com/phil-barrett/RP23CNC/blob/main/Photos/V0.95-top-assembled.jpg)

## Mar 1, V0.95 sent out for assembly.
Buck converter for 5V.  LDO for 1.1V.  Set up to experiment with other crystals than the pricey Abracon part. Added 4th digital input.
![V0.95](https://github.com/phil-barrett/RP23CNC/blob/main/Photos/PGA2350-v0.95.png)

## Beta boards have been sent.

## Features
- 5 Axis
  * Step, Direction, Enable outputs, 5V compatible
  * Limit Input with LED, 12V compatible
  * Servo Error Input with LED, 12V compatible
- Standard Grbl inputs, 12V compatible
  * Cycle Start, Feed Hold, Halt, Safety Door, Probe
  * LED indicators.
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
  * D0, D1, D2, D3
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


![V0.92 build](https://github.com/phil-barrett/RP23CNC/blob/main/Photos/T2120387_DxO.jpg)

## Status
Received first build of the board (2/10/2025). First test results: It boots and loads grblHAL firmware. Boot and Run buttons work. All inputs and outputs work. 12V isolated inputs work.  Prox sensors work. Step, Direction and Enable for all 5 axes work. 0-10V generation is good with excellent linearity. Ethernet (via the Wiznet module) works. Long job runs completed successfully. 5V regulator runs hot. Coming up: UART, I2C, SWDebug interface testing as well as more long job tests.

Key changes planned or considered.  
* The linear power supply for 12V to 5V needs to be changed. With the Ethernet adaptor, it runs at about 1W of dissipation which pushes the temperature to around 80C over ambient temperature. While this is still within the regulator's spec for most cases, the plan is to replace it with an SMPS.  The V 0.92 board is usable with Ethernet by using VUSB to feed 5V the 3.3V regulator. 
* V 0.92 uses the RasPi specified crystal and inductor (for the 1.1V) supply.  These are surprisingly expensive components that add a fair amount of cost to the final price so the plan is to move to using less expensive parts.
* Spacing of screw terminal increased by 0.08mm to allow easier assembly.
* SD Card adaptor moved to allow more reliable depanelling.
* Consider moving to a surface mount trimmer potentiometer to decrease cost (BOM and assembly).
* Consider making digital inputs 5V tolerant. (RP2350 inputs are 5V tolerant when powered at 3.3V, but not when the chip is unpowered.)
* Consider better handling of alternate UART 1 configuration.  Currently uses solder jumpers.
* One GPIO is available. Not sure what to use it for - digital input, digital output, ? Suggestions welcome.
* RP2354 variant has built in 2MB Flash memory. Want to support this and use the pins for GPIO. May require a fair amount of redesign.


![V0.92 build](https://github.com/phil-barrett/RP23CNC/blob/main/Photos/T2120352_DxO.jpg)

## Model Rendering
![RP2350B based RP23CNC](https://github.com/phil-barrett/RP23CNC/blob/main/RP23CNC.png)

## Main board features
![Features](https://github.com/phil-barrett/RP23CNC/blob/main/Documentation/features.png)
