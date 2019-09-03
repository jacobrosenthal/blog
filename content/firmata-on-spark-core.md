+++
date = 2014-08-31T02:42:00.000Z
title = "Firmata on Spark Core"
draft = false
in_search_index = true
aliases = ["/post/96225567522/firmata-on-spark-core", "/post/firmata-on-spark-core"]
[taxonomies]
tags = ["text"]
+++

[![image](/images/tumblr_inline_pbyzrsU7611rp3p4d_540.jpg)](https://www.flickr.com/photos/120586634@N05/14673011704/in/photolist-omB2bq-omwzMe-4t8Crd-4t8APG-esLdLY-nNWAfN-dRjK7x-6Dk9yk-ebRBh1-is6X3r-6gP4A8-jsTyrY-7u2D76-2FafUE-8MneV3-9vQVHk-bcq3W-98EEMH-98HNDy-98HNBU-9NJybd-9NGKrb-9NEtYQ-9NAsCc-9NFVNX-8DrQeq-9M2DZZ-9NKJWL-9NDvLH-6ATnuz-9NGabs-2gFEdE-6WZToY-9NEwpU-9NGBho-9NGYu8-9M2DUT-9NJKMw-98HNy3-iYsQzp-Hf8Hf-Hfbmv-Hf8J3-Hf8zA-Hfbwg-Hf8Cy-Hfbvx-6NAcR-HfbuB-kEbcaE)

[Photo Gareth Halfacree](https://www.flickr.com/photos/120586634@N05/14673011704/in/photolist-omB2bq-omwzMe-4t8Crd-4t8APG-esLdLY-nNWAfN-dRjK7x-6Dk9yk-ebRBh1-is6X3r-6gP4A8-jsTyrY-7u2D76-2FafUE-8MneV3-9vQVHk-bcq3W-98EEMH-98HNDy-98HNBU-9NJybd-9NGKrb-9NEtYQ-9NAsCc-9NFVNX-8DrQeq-9M2DZZ-9NKJWL-9NDvLH-6ATnuz-9NGabs-2gFEdE-6WZToY-9NEwpU-9NGBho-9NGYu8-9M2DUT-9NJKMw-98HNy3-iYsQzp-Hf8Hf-Hfbmv-Hf8J3-Hf8zA-Hfbwg-Hf8Cy-Hfbvx-6NAcR-HfbuB-kEbcaE).

As part of my work with the soon to be launched [Octoblu](https://www.octoblu.com "Octoblu") I've been working on porting Firmata over to [Spark Core](https://www.spark.io). The Spark's arduino abstraction has really come along making it the cheapest connected arduino out there, and me pretty excited about it.

<!-- more --> 

A firmata will allow us to command and control our sparks from all the existing firmata interfaces out there like Johnny 5 in Node or the many native interfaces. I should note Chris Williams has Voodoo Spark https://github.com/voodootikigod/voodoospark which is an RPC replacement for Firmata on Spark. From the Readme

"The VoodooSpark uses the Spark Cloud and its REST API to provide IP address and port information to the local spark core. It will then initiate a direct connection to the host machine, on which will need to be a TCP server. Once the connection has been made, the host machine can drive the Spark Core using the binary protocol defined below to effectively execute firmware API level commands dynamically."

That being said not relying on the Spark server or requiring you to have a TCP Server seemed like enough to bring Firmata over. Plus Ive been able to do things like tunnel firmata through mqtt which would allow Core sleep and store and forward messages that VoodoSpark currently couldnt achieve.

UPDATE: Firmata has forked the project for the Spark and I'm developing in dev at https://github.com/firmata/spark#dev with production being at https://github.com/firmata/spark

While a full working branch of octoblu (nea skynet) mqtt and core-firmware is over at  
https://github.com/jacobrosenthal/core-firmware/tree/skynet-mqtt-firmata

The branch is working for minor interactions, but theres still a bit to be done.
