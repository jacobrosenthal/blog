+++
date = 2014-11-24T06:14:13.000Z
title = "No more Arduino IDE - Program your Arduino from Node or Chrome"
draft = false
in_search_index = true
aliases = ["/post/103442586737/no-more-arduino-ide-program-your-arduino-from", "/post/no-more-arduino-ide-program-your-arduino-from"]
[taxonomies]
tags = ["text"]
+++

Today I built an [stk500v1 programmer in pure javascript](https://www.npmjs.org/package/stk500) freeing javascript folks from ever having to use the Arduino IDE (or avrdude) again. Instead:

npm install stk500  
node uno.js

<!-- more -->

As we continue to reach out and teach new people hardware through software with the [nodebots project](http://nodebots.io/) its become painful to have people download the Arduino IDE just to flash Firmata on their devices.

We're all waiting for Arduino to release their [web I](http://blog.arduino.cc/2014/08/12/news-and-updates-from-the-development-and-beta-testing-of-the-arduino-tre/)DE  (presumably open sourcing much of it?) but theres just no eta or guarantees there.

It struck me as odd this hadn't been done before and I think I know why now. Programming requires the dtr/rts control lines to reset the microcontroller. However, the popular and excellent [nodeserial](https://github.com/voodootikigod/node-serialport) from Chris Williams is the standard serial library for Node doesn't support [manual control of the rts/dtr](https://github.com/voodootikigod/node-serialport/issues/384) lines necessary for rebooting into bootloader mode.

As part of my work I added the [OSX bindings](https://github.com/jacobrosenthal/node-serialport/tree/controlsignals) to allow me to do just that. That means this only works on OSX right now. We'll need Windows and Linux bindings to get my fork accepted, so please jump in with those if you can.

Big thanks to the [Pinoccio](https://pinocc.io/) mesh Arduino Compatible project, especially their recently open sourced [js-stk500 project](https://github.com/Pinoccio/js-stk500). Large portions of my logic were lifted from the Pinoccio project's stk500v2 implementation. They've been stk500 programming in the browser for a year now. (Chrome's serial has supported control signaling for some time) The Pinoccio chip is based on the Arduino Mega though, which means their implementation was of the incompatible stk500v2 protocol and was unable to be used for Unos.

Next I'm working on browserifying and bringing my implementation back to the browser and I hope to work with Pinoccio to upstream my work and standardize further.

Until then, Ill see you all at [Robots Conf](http://2014.robotsconf.com/) in a couple weeks :)
