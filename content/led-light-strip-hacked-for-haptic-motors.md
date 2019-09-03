+++
date = 2013-08-27T15:18:00.000Z
title = "LED Light Strip Hacked for Haptic Motors"
draft = false
in_search_index = true
aliases = ["/post/59494035738/led-light-strip-hacked-for-haptic-motors", "/post/led-light-strip-hacked-for-haptic-motors"]
[taxonomies]
tags = ["text"]
+++

![image](/images/tumblr_inline_pbyzrsBFEt1rp3p4d_540.jpg)

Last week I got to talk at about my most recent hack, a flexible haptic strip that easy for anyone to use, at [Hack N Tell Round 25](http://www.meetup.com/hack-and-tell/events/133694432/) in NYC.

In between working for ASU's Cubic lab on a new [haptic](https://en.wikipedia.org/wiki/Haptics) strip, I was pondering ways to bring haptics more to the forefront. Sure you can buy a [bare motor](https://www.sparkfun.com/products/8449) or [lilypad motor](https://www.sparkfun.com/products/11008) from Sparkfun or elsewhere, but in practice they're a total pain to get working. You need a transistor and its a pain to mount them anywhere you'd want them -- Especially when motors are only really fun when you have a few of them to play with. And lets not even address the cost of say 10 of these modules!

<!-- more --> 

Then it hit me that the cheapest motor driver chip I could buy would be the <14cent [WS28XX](https://www.sparkfun.com/products/10444) series LED drivers that get used on LED light strips!

Now, it's not necessarily THAT novel to use LED drivers to drive motors. Many people, including myself, have done it before, but I realized theres no reason I couldn't use the same flex PCB process as LED strips as a form factor as well.

I don't yet know how to do flex PCB, and theres is no [OSHPark](http://oshpark.com/) for flex PCB yet :) (paging [laen](http://tmblr.co/my2XegkiW-uJSjdBo6WGf5A)) So I just found an [LED strip](http://www.ebay.com/sch/i.html?_trksid=p2047675.m570.l1313.TR11.TRC1.A0.Xws2801+strip&_nkw=ws2801+strip&_sacat=0&_from=R40) on ebay that used a common driver chip I liked, that wasn't integrated into the LED which is really common nowadays, and wasnt potted with epoxy or anything.

![image](/images/tumblr_inline_pbyzrtt4HH1rp3p4d_540.jpg)

The strips don't need many changes for motors. Just pulled the LEDs off and put a motor across one of the 3 channels, top to bottom. You can also add a little LED across one of these channels as well to get visual notification. Finally you'll want to use a multimeter to figure out which resistor hooks up to the motor so you can swap that resistor off for a shunt--You'll want as much current as the driver chip can give you. In the future you may want to add some motor protection with a flyback Schottky diode across where you put the motor to protect the LED driver chip.

The additional beauty is theres already a great Arduino library called [fastSPI](https://code.google.com/p/fastspi/) to run these! Just follow the directions for LED light strips. SCK to Pin 13, SDA to Pin 11. They should work on 3v or 5v but I've been running mine at 3v with more wearable Arduinos like the [Xadow](http://www.seeedstudio.com/depot/xadow-main-board-p-1524.html) and [Fio V3](https://www.sparkfun.com/products/11520).

And just like LEDs you can simply cut the strip anywhere you want, from 1 motor to 32, your choice!

We've tried them in baseball caps and arms and legs. I think they'd work well sewn into a bag strap. Let me know what form factor you try! And hopefully in the future I'll be able to get them produced for cheaper than hacking them from ebay :)
