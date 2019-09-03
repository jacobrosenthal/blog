+++
date = 2014-09-11T00:22:00.000Z
title = "Lightblue BeanBot"
draft = false
in_search_index = true
aliases = ["/post/97178122972/lightblue-beanbot", "/post/lightblue-beanbot"]
[taxonomies]
tags = ["text"]
+++

You've Probably seen [kilobot swarm videos](https://www.youtube.com/watch?v=xK54Bu9HFRw#t=19) going around.

[Luis](tiwtter.com/monteslu) wanted something fun to do with his [LightBlue Bean](http://punchthrough.com/bean/) so I set to turn my bean into a remote controlled swarm style bot.

{{ youtube(id="i1pIDjbR6YY") }}
<!-- more -->

 **DESIGN**

For construction I followed the rabbit hole to find the [original research for swarm bots](http://nereus.mech.ntua.gr/Documents/pdf_ps/ICRA206.pdf). Theres a lot of math, but the basics appear to be an equilateral triangle, 2 cylindrical motors opposite each other and the lowest possible friction so the vibrations can overcome it.

I tried a couple designs with common parts and came up with this design:

* Bean
* 3x ~30-50ohm resistor- bigger better because less current and longer battery life, but at some point the motor wont turn on...
* Hot glue
* Scrap <.5 inch diameter, >.5 inch thick to stick motors to safely (for me it was a laser cut scrap hexagon)
* 2x 3v 10mm pancake motors

For the resistors, basic math said had to be around 20-100 ohm resistor. I tried some out and was seeing about 1v drop across motor. Using an LED calculator presuming our 3v coin cell battery source, and wanting less than 40ma (arduino pin limit) of current you can [calculate for our 50-100ohm resistor](http://led.linear1.org/1led.wiz). I've found some motors are finicky to turn on at such low voltage though so I consider 30-50ohm the appropriate resistor.

NOTE: Before the engineers write in, yes I know we should have [flyback diodes](http://en.wikipedia.org/wiki/Flyback_diode) and frankly shouldnt stress the microcontroller pins as close to max current as we might be. We're not selling these things to the government. We'll be fine..

**ASSEMBLY**

Always remove the battery before operating on the bean. Its VERY easy to bridge stuff and you dont want to be done before we've started.

We're using the resistors as legs to keep part count down and remove the need for jumpers or other wires. Note this means that the legs are live with voltage. Don't touch them to eacother or let them touch the rest of the board and dont drive on metal surfaces. But frankly with the Bean not in an enclosure you should be mindful of all that normally. Solder one of each to the A0 and D5 holes. Sadly theres no more holes near the center of gravity, so hot glue the third resistor the battery side which we'll call the front.

Most motors have tape on them otherwise get some double sided tape and put the motors on either side of the spacer and tape it to the top of the ble chip. Again be careful not to touch metal to metal, use extra tape to protect if need be.

Now solder down the same color wire on each motor to its nearest gnd pad. which ever color you pick will be if your bot drives 'forwards' or 'backwards', whatever that means. For me blue to resistor meant forward was toward battery and third leg resistor. Solder the other wire of each motor the top of the resistor.

Now you can bend the legs as you like. You're going to have to play with them to get leftish, rightish and straightish motion so dont worry about it too much right now.

**USE IT**

[Previously I've been working with firmata on bean over ble](http://citizengadget.com/post/96226562047/firmata-on-lightblue-bean). This has allowed me to develop js apps that can control my bean from the browser, mac, or mobile with the same codebase.  I think you can control pins from the bean iphone app, but I can't figure it out :)

*UPDATE* Luis has a post on [using node.js to control beans cross platform including mobile with phonegap](http://blog.iceddev.com/2014-09-15-beanbots-rise-of-the-swarm.html).

**FEEDBACK**

Let me know what you find. Does bending the legs a certain way lead to better results. Can you find a better common leg material? Care to program some swarm behavior? I'm [@jacobrosenthal](https://twitter.com/jacobrosenthal) on twitter

**STEERING *UPDATE***

I've found it can be tough to change steering by just bending the resistors. Feedback so far has been that changing the resistor can be a more effective way of steering. If one of your motors seems to go, say, right really well, and the other goes only a little left or actually a little right, you can try lowering the resistor for that motor so it gets more power to pull that direction.
