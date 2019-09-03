+++
date = 2014-01-29T06:43:00.000Z
title = "iFirmata now in the App Store"
draft = false
in_search_index = true
aliases = ["/post/74921242754/ifirmata-now-in-the-app-store", "/post/ifirmata-now-in-the-app-store"]
[taxonomies]
tags = ["text"]
+++

![image](/images/tumblr_inline_pbyzrs64Xy1rp3p4d_540.png)

[iFirmata](http://ifirmata.github.io/) hit the Apple [app store](https://itunes.apple.com/us/app/ifirmata/id795905884?ls=1&mt=8) today! iFirmata lets you connect to your Arduino to your idevice via a BLE connection ([Xadow](http://www.seeedstudio.com/depot/Wearable-t-7.html?filter2=1&ref=top) or [RedBear](http://redbearlab.com/bleshield/) currently) using the awesome open source [Firmata](http://firmata.org/) protocol.

It lets you connect to your Arduino and do all the things you could normally do over the wire with Firmata including digital write a pin high or low, read analog values, set PWM or servos, send i2c commands to devices or trigger custom scripts using the send string function.

Check out [this hastily made video](https://www.youtube.com/watch?v=Wv58Vw8H8tQ) that I had to do in order to get Apple to approve it.

Of note, I put a $5 dollar price on it. Besides the months these side projects of mine are taking, dealing with the app submission is getting to be tiresome and my new resolution is to never put something in the store for free without a very good reason. If you know what Firmata is you're probably interested and willing to throw me 5 bucks. If not its all up on [G](https://github.com/iFirmata/iFirmata)ithub so grab a copy and build your own. And when you're done prototyping grab my source and make your own app. If you're REALLY poor [contact me](http://jacobrosenthal.com/contact.php) for a promo code.

Of note, you CAN get Firmata to connect over BLE on a Mac by using 10.8 or greater and pairing your BLE device which binds a tty. However, thats a bit hacky at least for application usage. My implementation should work on macOSX with very few changes but I haven't gotten to it yet. Send me some pull requests to kick me in the butt.
