+++
date = 2014-04-23T09:43:00.000Z
title = "Advanced Pinoccio"
draft = false
in_search_index = true
aliases = ["/post/83605797713/advanced-pinoccio", "/post/advanced-pinoccio"]
[taxonomies]
tags = ["text"]
+++

In doing some work recently I had the pleasure of obtaining a bunch of new <http://www.pinocc.io> scouts -- Internet of Things Arduinos! The Lead Scout has wifi and talks to the other scouts nearby via mesh networking (non compliant Zigbee sadly). After playing around a bit I came to the conclusion that I liked the hardware. As opposed to the Spark, these are truly Arduinos. In addition to a nice webshell (via bitlash) and set of API's you can write code as you normally would right within in the Arduino IDE. This is in stark contrast to the [Spark](spark.io) which emulates Arduino from an as yet unfinished web IDE where libraries are largely not yet ready. It's worth noting that I think the Spark is my long term bet, but in the short term our hackerspace has been lousy with the Spark and nobody's doing anything with them. That said I found the prototyping shield not enough room to play in. I wanted a full development environment so I set out to create one.

  
**How to run Pinoccio in Atmel Studio 6.2 (IE for simulating and step by step debugging):**

<!-- more --> 

Make sure you have the Arduino files (go with the [nightly build Pinoccio recommends](https://pinocc.io/solo)) installed at: C:\Program Files\Arduino

and the [Pinoccio libraries](https://github.com/Pinoccio/firmware-pinoccio) and hardware installed at:  
C:\Users\XXXX\Documents\Arduino

Now for the Atmel Studio setup. The full description for how to do this in general is [up at Engblaze](http://www.engblaze.com/tutorial-using-atmel-studio-6-with-arduino-projects/), but I've done the hard work and [uploaded a completed 6.2 solution to Github](https://github.com/jacobrosenthal/pinoccio-atmel-studio).

Unzip it to C:\Users\XXXX\Documents\Atmel Studio\

Open it up and you should be able to simulate and debug your bootstrap code!

  
**How to burn an Atmega256rfr2 Xplained Pro or other breakout as a Pinoccio from within Atmel Studio**

Atmel makes a breakout for the Atmega256rfr2 called the [Atmega256rfr2 Xplained Pro](http://www.atmel.com/tools/atmega256rfr2-xpro.aspx).  It doesnt have the Fuel Guage, or FTDI chip for serial communication, but its a great breakout with onboard debugger and plenty of room to work.

First, you'll need to set the fuses. [Look them up](https://github.com/Pinoccio/core-pinoccio/blob/master/avr/boards.txt) and set them in Atmel Studio.

Other than that everything is the same as above except I had to make one change to halFuelGauge.cpp because it'll hang trying to talk to our non existent fuel gauge:

unsigned int HAL_FuelGaugei2cRead16(unsigned char address) {  
int data = 0;

// Wire.beginTransmission(MAX17048G_ADDRESS);  
// Wire.write(address);  
// Wire.endTransmission();  
//   
// Wire.requestFrom(MAX17048G_ADDRESS, 2);  
// while (Wire.available() < 2)  
// ;  
// data = ((int) Wire.read()) << 8;  
// data |= Wire.read();

return data;  
}

Now just burn that image.

To actually talk to the board you'll need to add an [ftdi friend](https://www.adafruit.com/products/284)

From the [Pinoccio definitions](https://github.com/Pinoccio/core-pinoccio/blob/master/avr/variants/pinoccio/pins_arduino.h) we know the serial pins are RX to PE1 and TX to PE0 and black to GND.

Now you can open up your serial port and you'll see the bitlash command prompt just like it was a real Pinoccio!

NOTE: if you want opening serial to reset the board, you're going to have to add in the reset line. Note, however, you'll need a .1uF capacitor between your RTS on the ftdi friend and the RSTN pin.

  
**How to have your Atmega256rfr2 discovered by HQ as a real   ~~boy~~ Pinoccio**

This is pretty difficult. Before you go any further, know even I haven't successfully done this yet.

First you need to buy and hook up a MAX17048 / MAX17049 fuel gauge breakout. Test without the code from the previous section commented out and make sure it all works, or at least doesnt freeze the sketch trying to find it.

Next, you need to have the bootloader burned on to your Atmega256rfr2. 

You can find a hex to burn from Atmel Studio in the [Pinoccio Github](https://github.com/Pinoccio/core-pinoccio/tree/master/avr/bootloaders/STK500RFR2) and again make sure to [look up](https://github.com/Pinoccio/core-pinoccio/blob/master/avr/boards.txt) and program the fuses as before.

Or you can hook up an ISP programmer using [the pin definitions](https://github.com/Pinoccio/core-pinoccio/blob/master/avr/variants/pinoccio/pins_arduino.h) as guide and burn it right from Arduino, knowing it'll get all the fuses itself.

Now that you have a bootloader you can upload the Examples->Pinoccio->Bootstrap sketch right from Arduino.

Finally you'll need to either edit the Pinoccio HQ Chrome Extension with your FTDI's PID and VID set to be Pinoccio (VENDOR_ID 0x1d50, PRODUCT_ID = 0x6051), or burn a new PID and VID to your FTDI with [FT_Prog](http://www.ftdichip.com/Support/Utilities.htm). Since Burning a VID and PID didn't work for me (the drivers still didn't really think it was a Pinoccio) I'd suggest the Chrome Extension route.

Go to Chrome Extensions, and turn on Developer Mode in the upper right corner. Then find Pinoccio. Disable it and look for its id like njhfipeehmigebbdfbingghcjdfmjeai.

On my Mac I found the files at  /Users/XXXXX/Library/Application\ Support/Google/Chrome/Default/Extensions/njhfipeehmigebbdfbingghcjdfmjeai and copied the version named folder out to the Desktop.  Windows folks should find their folder in a more Window-sy location.

Now edit the manifest.js file to add your FTDI's vendor and product ID like so  
"usbDevices": [ {  
"productId": 24657,  
"vendorId": 7504  
} ,   
{  
"productId": 24577,  
"vendorId": 1027  
}  
]

Next, open up the pinoccio.js file and swap out the pid and vid at the top for yours.

Now, back in Extensions, click the load unpacked extension and select your file.

Lastly, you'll need the capacitor on the reset line as described above because the Extension will want to reset the board. 

Now head to <http://hq.pinocc.io> It should find your device, decide its out of date, and hopefully successfully contact the bootloader to upload a new Bootstrap copy (hence the need for us to have a working fuel guage since we don't have room to comment anything out here)

Let me know if you get this to work, as again, I haven't!
