Welcome To: LeoEc Basic Example Firmware!!
================================

##### Note: This is for the LeoEc Hardware Version 1 Branch

This is the base example sketch for using LeoEc hardware.
It outputs data via USB serial but can easily be modified to use Serial1 as well.

Reading eC just got a bit easier
-------------------------

As before reading eC has never been easier, and with the new hardware version so it agumenting LeoEc!
All Standard Leonardo pins are brought out via the Digital Header and Analog header!

Simply plug in LeoEc via a USB port, point you favorite Serial Port monitor to LeoEcs port and off you go! 
**LeoEc even works on openWRT flashed routers for eC readings over Wifi!**

Please see [LeoEc's Project page](http://www.sparkyswidgets.com/portfolio-item/LeoEc/) for more information!
<http://www.sparkyswidgets.com/portfolio-item/LeoEc/>

Whats in the firmware?
-------------------------

This is a really basic start to reading eC with the hardware, I am posting it up to help speed development, if you have better version please please issue a pull request and I'll merge in your improvements!

Installation Info
-------------------------

With the newer version of the IDE I feel its easiest to download and use the LeoWQS (Water Qaulity Sensors) version of the IDE I maintain a build on all 3 platforms(OSX, Linux, Windows)
##### Some of the changes needed (pretty standard to adding variants to Arduino) 
- I am know using the aduino.inf driver file on windows, although unsigned it should work on win 8 as well
- All changes to the IDE are included in the build.
- for those interested to add a Leonardo type board to the IDE you need to do a few things
--* You'll need a VID/PID combo, and assuming you have one or can get one(openmoko, camp defunct company, buy one)
--* Add your **bootloader PID** into the bootloader, there are a few variations of the LUFA I generally use a default Caterina but do makes some changes
--* Add you information into the descriptions portion of the bootloader, and also adjust you uploaded and heartbeat LEDs if needed!
--* in the IDE you will need to add your information into USBCore.cpp (hardware/cores)
--* add reference to your boards in the AVRDudeUploader.java file, this will allow the triggering the special autoreset on leonardo type board. This is th major change people miss!
--* Makes sure your boards.txt contains the proper VID and **Sketch PID** combo not the bootloader PID (example, if sketch PID is x1234 bootloader PID is x0034)
--* its best to use a variant, you could even use a separate core to avoid collisions with Arduino's own new boards

**Even better see my Arduino Fork where I keep these changes up to date with the newest versions of Arduino!**
<https://github.com/SparkysWidgets/Arduino>

Basic Usage
-------------------------

Usage of LeoEc is very easy, with on board USB a fully CDC compabtible bootloader (modified leonardo) all you need to do is plug it in and send some serial commands! Send an S to calibrate to eC LOW solution, F to calibrate to HIGH an R to read and etc...

There are 2 serial ports one for the USB and one is the hardware serial port(Tx,Rx), this makes it useful as a USB to serial converter as well, but also means that the proper port must be select for use in any project. For example a Raspberry pie could interface LeoEc(careful on levels) over USB serial while the same data is dumped over the Hardware Serial to another Arduino. An I2C slave example code is also implemented which uses some of the same commands and shows how to easily implement a eC sensor with an I2C interface!

####Some of the commands are:
- C : Continuous Read Mode: Dump readings and data every second
- R : Single eC reading: response "eC: XX.XX" where XX.XX is the eC
- E : Exit continuous read mode
- S : set eC LOW Calibration point
- F : set eC HIGH Calibration point: also recalcs probe slope and saves settings to EEPROM
- X : restore settings to default

Hardware: Schematics and Layouts
-------------------------

- Take a look in [LeoEc's Hardware Repo](https://github.com/SparkysWidgets/LeoEcHW) for the EAGLE files!
- Check out my I2C pH interface[MinipH](http://www.sparkyswidgets.com/portfolio-item/miniph-i2c-ph-interface/) for a really cost effective pH Probe interface!


License Info
-------------------------

<a rel="license" href="http://creativecommons.org/licenses/by-sa/3.0/deed.en_US"><img alt="Creative Commons License" style="border-width: 0px;" src="http://i.creativecommons.org/l/by-sa/3.0/88x31.png" /></a><br />
<span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">LeoEc</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="www.sparkyswidgets.com" property="cc:attributionName" rel="cc:attributionURL">Ryan Edwards, Sparky's Widgets</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/3.0/deed.en_US">Creative Commons Attribution-ShareAlike 3.0 Unported License</a>.<br />
Based on a work at <a xmlns:dct="http://purl.org/dc/terms/" href="/portfolio-item/LeoEc/" rel="dct:source">http://www.sparkyswidgets.com/portfolio-item/LeoEc/</a>