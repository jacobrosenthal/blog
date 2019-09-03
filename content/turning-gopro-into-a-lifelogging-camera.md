+++
date = 2012-10-17T09:55:00.000Z
title = "Turning GoPro into a lifelogging camera"
draft = false
in_search_index = true
aliases = ["/post/33765926832/turning-gopro-into-a-lifelogging-camera", "/post/turning-gopro-into-a-lifelogging-camera"]
[taxonomies]
tags = ["text"]
+++

![image](/images/tumblr_inline_p1w4ebdcsp1rp3p4d_540.jpg)

Recently my hetero life partner [Colin Ho](http://colin-ho.com/) and I turned a GoPro Hero into a lifelogger camera.  I've wanted to do life logging forever but never got my stuff together so when Colin brought in the camera in and made the challenge, I was in.

<!-- more -->

Take a look at [Colin's post](http://colin-ho.com/the-lifelogger-camera/), but basically,  we pulled some code, schematics and a pinout from [this guy](http://chargeconverter.com/blog/?p=71) and set to implementing it all in one night at our hackerspace [HeatSync Labs](http://www.heatsynclabs.org/). I laid out the board in Eagle and etched it Colin did up all the mechanical designs (laser and 3d printed). The only speciality part we needed was an iPhone connector which, since this is a hackerspace, we had stashed around ;) The result is hosted on [Our Git](https://github.com/Augmentous/LifeLogger).

Colin has been using the camera for ~3 weeks while traveling and Ive been using it for about a week. In my tests at approximately 2 pictures per minute I'm getting 18h hour battery life on a used old GoPro Hero.

The daylight results are awesome. The camera placement with the fish eye lens is perfect. Im picking up conversation partners, meals, a great view of my laptop, phone, and any projects I'm hacking on.

![image](/images/tumblr_inline_p1w4iprIaj1rp3p4d_540.jpg)

The only problem is blurriness in ~50% of shots. Basically without knowing if the shot is being taken we're not staying still. We may want to turn on the GoPro's audible beep again, or do something light or haptic based to notify of the impending shot, but theres an argument for not changing my life or becoming aware of when shots are being taken.

![image](/images/tumblr_inline_p1w4j0t7ps1rp3p4d_540.jpg)

The real drawback so far has been the low light response which is TERRIBLE. Blurriness probably goes up over 75% especially if theres ANY motion. For a worst case scenario I took it out to a nightclub (where I drank and danced way too much for photos anyway) and only got maybe ten usable photos out of a thousand!

![image](/images/tumblr_inline_p1w4jdcZ6U1rp3p4d_540.jpg)

This was an average GOOD shot! Still, I got ten awesome photos I wouldn't have had otherwise.

To get around this I'm going to up my shot rate and expect to throw away half of my photos. Related: Anyone seen anything to detect and rate photos based on focus?

Take a look at more results over at my ~~flickr~~ [new server!](http://jjrosent.zrg.cc/?user=jacob/eyefi1)

Of note, the Hero 3 was just [announced](http://gopro.com/hd-hero3-cameras). It is half thickness from the Hero 2 and can do eight hours on intervalometer so we may just be able to use that camera out of the box without external modification. However, there may still be a reason for us to add some buttons and lights to make the hero a frendlyier life cam.  We're certainly happy enough with the results to keep playing!
