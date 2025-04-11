# RP23CNC
RP235x based breakout board for grblHAL.

[Features](https://github.com/phil-barrett/RP23CNC/blob/main/Documentation/featurelist.md)

![V1.0 build](https://github.com/phil-barrett/RP23CNC/blob/main/Photos/RP23U5XBB-V1.0-angled.png)

## April 10
### Update to user manual
All that is remaining is the assembly section (waiting for actual boards for photos and a bit more in the Servo section. And, more proof reading and polishing, of course.

## April 9
### Tariffs and the future of the RP23U5XBB
The ongoing chaos in international tariffs has been, honestly, very unsettling.  The changing tariffs - 30%, 54%, 104%, 125% - make it impossible to plan for.

So, after more than a couple of days being stuck by all this craziness, I decided to get moving forward and let the chips (er, tariffs) fall where they may.  I have sent V1.0 out for the first production run. When I get it back and factor in all the costs, I will announce pricing. Not the best way to run a business but I want to make this board available.

The changes to V1.0 are, as suggested earlier, to UART1 and Aux2/PWM configuration via solder jumpers.

V1.0 rendering is shown above. Photos will be shown when we receive the boards from the production run.

## Mar 31
### More work on the User Manual
Continuing to add more information.  Some reorganization.

### Minor Tweaks continue.
I am concerned that there are too many pin header jumpers on the board at this point.  I may drop one or two and replace with solder jumpers. In particular, I believe the PWM/Aux2 pin header jumper is an infrequent option and can be relegated to a solder jumper, defaulting to Aux2. Maybe DI3/UART 1 is the same way - default to UART 1.

## Mar 30
### Big Update to User Manual
Whew! That was a lot of work.  Lots of new information. Waiting for final 1.0 board to put a BOM in.  I went over it carefully but there are probably still some typos and errors.

### V0.96 looks good
I have made a few minor tweaks. Silk screen and connector positioning.  No errors found yet.  Still planning for a mid-April release. One last thing I am considering is to add solder jumpers to all the pin header jumpers.  This would allow (but not require) solder closure of all jumpers.

## Mar 27
### V0.96 boards received
Initial tests look good.  All the modifications from V0.95 verified. Now on to a full battery of tests.  

## Mar 20
### V0.96 send to the contract manufacturer
I am fairly confident this is the last beta build. I'm going to be on vacation for a week and when I get back the boards should be there too.  I'll do another series of tests and, if good, will be sending off for a production run. Hopefully the RP23U5XBB will be available for purchase in mid April. I will be on-line this coming week, by the way.

## Mar 19
### More UART thoughts
Looking at how UART1 shares pins with the digital I/O section. The configuration options are too confusing. I will remove the ones from the bottom of the board and connect TX directly to the RP2350 pin. On top, I will have a 2 way jumper (3 pin) that can be used to select RX or Digital In 3. This prevents the possibility of 2 external devices coming in conflict (one driving the pin high, the other low).

### General usability and cosmetic cleanup
Did general clean up in preparation for the third build, V0.96. Silkscreen tweaks, word smithing. Moved Spindle LED to a cleaner location.  Changed Aux_Out_2/PWM selection from 0R resistor to 3 pin header to be consistent with other similar selections and more user friendly. I am hoping that this will be the final pre-release build.

## Mar 18
### UART Day!
Spent some time testing the UARTs. UART0 got a throrough workout and appears to be fully functional.  I tested both 3.3V and 5V operation. The test set up used a second microcontroller as a receiver/sender.  The two applications (basically the same progam) passed large amounts of data back and forth. The tests were run at 4 different baud rates: 115200, 230400, 921600 and 1228800.  Yes, it passed the test at 1.2 megabaud, even with 5V translation.

Sadly, I found a bug in the board. I connected to the wrong pin for UART1 TX - Aux_out_0 instead of Aux_out_2. Sigh. I was able to access the correct pin and verified that UART1 worked but did not run the full battery of scenarios as on UART0.  It's an easy fix but full testing will have to wait for the next turn of the board. This does mean that Aux_Out 0 and 2 pins at the RP2350 are swapped. The plan is to send it to the contract manufacturer on Thursday.

## Mar 17
### More beta boards shipped

### Relay Testing Update
I was able to torture test with both 5V and 12V relays on both V0.92 and V0.95.  In both cases I tested using the ULN2003 drivers and also driving the coils directly from the 5V and 12V rails.  The latter is not a recommend use of the board power rails because they don't have kick back diodes but I wanted to see what the kick back does to the various power rails.  Short story, it isn't pretty. The ULN2003 does have kickback diodes so it is cleaner. But, in all cases, the board and USB connection did not fail. 

My methodology for each test was to wire the relay coil in so I could manually trigger the relay with one of the wires. This allowed me to do hundreds of relay cycles very quickly.  For the power rail test, I wired one of the coil terminals to the rail ground and then the other wire to the positive rail (+5V or +12V, depending on the test) but not to the other coil terminal. I would touch that wire to the other terminal to trigger the relay.  There is an audible click as it closes. Similarly, when it opens. For the relay driver, I used the spindle enable terminal. I wired one wire from the +V terminal to a coil terminal and the trigger wire to the signal terminal. When the spindle is on, I can touch the other end of the wire to the other coil terminal to trigger the relay.

There were 6 test cases per board version: 
- USB 5V rail
- USB 5V driver
- Board generated 5V (LDO or Buck) rail
- Board generated 5V (LDO or Buck) driver
- 12V rail
- 12V driver

I started a job running and then triggered the relay at least 200 times in each case.

Looking at the power rails on a scope, the rail tests were ugly on 5V and 12V but 3.3V (IO VDD for the RP2350) was surprisingly clean. God bless our stalwart low dropout voltage regulator! The full compliment of by pass capacitors on the RP2350 didn't hurt either. The driver tests had some fluctuations on 5V but, again, the 3.3V rail was clean. In all 6 cases on both versions, grblHAL ran without any problems during the tests. So, at this point, I do not plan any changes to the power section of the board. Glad to put that one to bed.

## Mar 15
### Beta testing
Added several new beta testers. They will get V0.95. 
Chasing a power management worry with 5V relays. Not sure it is a problem with the board. Could be ground bounce.

### V0.96 coming together
Changed the USB connector to a USB-C.  Added more test points for "bed of nails" testing. I am hoping this will be the final build before production.  Planning to send it out mid next week.

### Board test system work 
Received the Board Test controller PCB and assembled it partially (don't have the I/O expander chips yet, come on Mouser, fix your slow order processing system). Looks good so far.

### Added VRML and STEP models
Fully populated boards in a single zip file. See 3D Model section. 

## Mar 14
### Beta testing feedback
Several issues have been reported but mostly it is fairly clean.  Good news from a highly technical tester - after one bug fix there are no lost steps and low low jitter even at fairly high step rates. 

### Looking to add some more testers.
I am looking to expand the list of beta testers a bit more. The profile of an ideal tester:
- Is familiar with grblHAL or Grbl
- Has a CNC machine that they can drop the board into
- Has a servo based CNC machine to test with (for testing the servo alarm inputs).
- Is willing to spend the time to install the board and work with me on any issues that might arise

Not having all those is not a deal killer, by the way. As a bonus, you get to keep the board. No cost to you. Please contact me on the beta testers wanted thread in the Discussions section.

### Board test system work 
The Board Test system design work is coming along well. More of the issues have been worked through and I am close to sending the base board out for the first build. These are always tricky to design because of the need to have the pogo pins on base align with the actual board. Plus, you have to think differently about how to exercise all the I/O, test power voltages (there are 5 on the board) and generally do it quickly so board testing doesn't consume a lot of time. And, you have to design a test fixture that will hold up to many test cycles.

## Mar 10
### Long term burn-in on V0.95 boards
Looks good.  No problems found.  Board temperatures all within expected ranges. Will be doing limit testing on the power subsystems.

### Board test system work
I will be using a bed of nails test approach with a Pogo Pin Test Board (PPTB) design for testing.  Decided to go with a test program that runs on the DUT (RP23U5XBB) connected via the PPTB to work with a Board Test Controller (BTC) based on a Teensy 4.1. The DUT will self-test 12V I/O, digital I/O, cycle the BOOT/RUN pins, cycle the stepper pins and communicate results with the BTC via UART0.  The BTC will verify voltage levels, test stepper outputs (in conjunction with the DUT FW) and control the Boot/Run pins. A Linux program will load firmware on the RP2350B (test program and a version of grblHAL), tell the BTC to start the test, receive PASS/FAIL notification and optionally print a report. Probably based on a RaspPi. The overall design is a work in progress and there are still a few loose ends to nail down..

Finished Board Test Controller (BTC) design.  Decided to assemble it myself - sending off for PCBs. Here's a rendering.
![V0.95](https://github.com/phil-barrett/RP23CNC/blob/main/Photos/test%20driver.png)

Still working on the Pogo Pin Test Board (AKA, bed of nails tester). This is always a bit tricky to do but a fun challenge, none the less.

## Mar 7, V0.95 boards back.
Using LDO to generate 1.1V works. Alternate crystal works. 5V buck generation works pretty well. Testing shows buck converter runs at about 10 C above ambient while running a long term test with LED loads on step signal output. Heat imaging shows no hot spots. Made decision to move to USB-C connector.  
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
