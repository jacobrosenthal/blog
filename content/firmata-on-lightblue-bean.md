+++
date = 2014-08-31T02:55:00.000Z
title = "Firmata on LightBlue Bean"
draft = false
in_search_index = true
aliases = ["/post/96226562047/firmata-on-lightblue-bean", "/post/firmata-on-lightblue-bean"]
[taxonomies]
tags = ["text"]
+++

![image](/images/tumblr_inline_pbyzrshEbi1rp3p4d_540.jpg)

Another day, another Firmata fork. I spent the last few days messing around with getting Firmata working on the [LightBlue BLE Bean](http://punchthrough.com/bean/). I had previously written the [Node NPM package for the Bean](https://www.npmjs.org/package/ble-bean) as an exercise to get to know both Node and the Bean. Why not give it full Firmata control?

You need firmata on your bean from [my clone](https://github.com/jacobrosenthal/arduino/blob/bean/examples/StandardFirmata/StandardFirmata.ino) and [@monteslu](https://twitter.com/monteslu) has put together a [node example turning my bean package into a serial port and hooking it to firmata.js!](https://github.com/monteslu/bean-serial/tree/master/examples/firmata)

<!-- more -->

The big gotchas Ive found so far are is that Punchthrough actually moved pins around in pins_arduino.h. There should be a fix for this but Standard firmata writes pins in order on the port.. So for now I'm just using the true pin names which map like so:

a0 -> a4->d18
a1 -> a5->d19
d0 -> d6 -- Unavailable right now from firmata
d1 -> d9 -- Unavailable right now from firmata
d2 -> d10
d3 -> d11
d4 -> d12
d5 -> d13

Beyond that I would avoid all other pins which still exist and could be hooked up to anything for all I know. This sketch doesnt protect any pins. Setting anything else very well may take your bean offline or worse..

Other than that I just added Bean.sleep at the end of loop to allow bean to sleep for power saves. Adjust to taste.

Besides resolving the pin mapping, theres plenty to be done to make this a full port. There should be a more clear Firmata Boards.h entry to show the true available pins, and in Standard firmata we might look to protect other pins from being touched. I also havent tested servo/pwm/etc functionality, especially with the sleep addition...

Note -- I've been using [firmata.js](https://www.npmjs.org/package/firmata) for my Node firmata needs but we've found some problems with how chatty it is out of the box. It was designed for a serial cable world and we're quickly moving past that, though our PRs arent being accepted.  @monteslu has a [firmata.js fork](https://github.com/monteslu/firmata/tree/nohandshake) up that we're now using exclusively
