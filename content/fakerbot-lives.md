+++
date = 2011-03-01T07:00:00.000Z
title = "Fakerbot Lives"
draft = false
in_search_index = true
aliases = ["/post/169172396142/fakerbot-lives", "/post/fakerbot-lives"]
[taxonomies]
tags = ["text"]
+++

[This post is from our [3dprinting wiki](http://wiki.heatsynclabs.org/wiki/Fakerbot) and is being added here and backdated for completeness]

The machine is called a FakerBot, because it's not quite a MakerBot, but there is a direct lineage. Since we didn't have access to a laser-cutter and we wanted to do it on the cheap, the frame was slightly redesigned by Corey so that it could be cut on a tablesaw from inch material. The tongue and groove construction was replaced with dado-cut slots. All holes were made with a 7/8" forstner bit, this allows them to take a skate bearing (a paper shim is required) or anything else that we wanted through the use of adapter plates since we knew that mods were likely. Total cost of the enclosure was $13 for a sheet of 1/4" (actually 5.2mm) Luan from Home Despot which provided enough material to make four FakerBots even though we only made one. A laser-cut frame would have cost about $200 form Makerbot, so we saved a lot here. The frame was finished with linseed oil and came out pretty nice. MakerBot specified precision shafting for the X&Y axis which is unnecessary for a low-tech motion control system like this one. Drill rod was substituted for all linear shafting at a total cost of about $3 which is another $20 or $30 reduction. Similarly, low-cost nylon bushings were substituted for the more expensive MakerBot spec'd parts. The X and Y stages on the MakerBot are pretty good aside from being too tall, however the Z-stage is a horrible design. It is overly complex, wobbly, prone to jamming, etc. A replacement z-stage was designed by Corey with the goal of making Z simple and reliable:

 **The following parts from the Makerbot design were removed:**

  * (1) Belt
  * (8) Bearings
  * (1) Driving Pulley
  * (4) Driven Pulleys
  * (2) Idler Pulleys
  * (1) Platform
  * (2) Extruder Mounts (Dragons)
  * (4) All-thread Rods (leadscrews)
  * (4) Driven nuts (leadnuts)
  * assorted screws and hardware



 **That giant steaming pile of hardware was replaced with:**

  * (1) 1/4-20 Acme leadscrew
  * (1) Antibacklash nut
  * (1) shaft coupler
  * (1) Cantilever arm (laser cut)
  * (1) Linear rail
  * (1) Truck for linear rail



  
 **An overall reduction from (27) functional components down to (6) !**

  
If you count every nut and screw the reduction is far greater, but you get the idea. The new Z-stage is a big improvement and has eleminated all of the jamming and wobbling problems that we had previously. It also looks far better.

The extruder is Corey's design hosted at <http://www.thingiverse.com/thing:4579>. It is a clean-sheet of paper design that sprang from the frustration of dealing with the shortcomings of other extruders. So far the CoreyStruder and its derivatives have been downloaded on Thingiverse over 250 times.

The hot-end is Corey's copy of the hot-end used on the UP! printer which he later discovered is actually a copy of Nophead's design. It is very compact and works well. Nophead does awesome work, his blog is a must-read:

<http://hydraraptor.blogspot.com/>
