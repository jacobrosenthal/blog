+++
date = 2012-04-10T07:00:00.000Z
title = "Festival of Creativity Desert Playground Recap"
draft = false
in_search_index = true
aliases = ["/post/170845279782/festival-of-creativity-desert-playground-recap", "/post/festival-of-creativity-desert-playground-recap"]
[taxonomies]
tags = ["text"]
+++

![](/images/tumblr_inline_p43v98yX0z1rp3p4d_540.jpg)

This past winter 2011 [Tim Gerrits](http://doteki.com/?page_id=96) and I were lucky to be invited to work with Boyd Branch, Daniel Roth and Southwest Scrap Exchange on a small arts center grant for [Mesa Festival of Creativity 2012](https://www.mesaartscenter.com/spark). The grant concept was a “Desert Playground” which we ended up interpreting as a series of interactive cactuses utilizing Southwest Scrap Exchange creative reuse. 

* * *

We brainstormed several different cactus concepts (my favorite that didn't make it was a tumbleweed style cactus via a [hamster ball prototype](https://www.flickr.com/photos/hslphotosync/6610769033/) ) but I mainly worked on a motion sensitive pool noodle agave (above) 

The whole project was incredibly price sensitive and for a long time I couldn’t figure out how to afford enough motion sensors to enable interactivity in so many leaves. Tim Gerrits ended up inventing a very clever cheap motion switch based on a spring, copper tube and ball bearing.

![](/images/tumblr_inline_p43wj0lp3u1rp3p4d_540.jpg)

With so much wiring I wanted clean consistent connections so I fabbed a mosfet driver screw shield to break out an Arduino Mega for its large amount GPIO. I brainstormed with Jasper a simple [fall off algorithm that loaded a random number into an array upon motion, then just slowly shifted the bits off until the cactus eventually settled back to stillness](https://github.com/jacobrosenthal/Agave/blob/master/code/agave_final.ino). We also added an attract mode so it would freak out if left alone too long.

The Prickly Pear was the last to come together and became much more art the science.

![](/images/tumblr_inline_p43w7k9MVb1rp3p4d_540.jpg)

We developed a concept of ‘flowers’ [that would slowly ‘die out’ when plucked](https://vimeo.com/49778644). I wound coils and hid them in the agave paddles and wired them down to the same mosfet power shield we used in the Agave.   


![](/images/tumblr_inline_p43wlxhWDX1rp3p4d_540.jpg)

Then I wound another coil around 20oz plastic bottles ‘flowers’. I swapped out caps until I had decent coupling to transfer enough power to light up an led from ~6 inches away.

Grant based art work is incredibly grueling and I gained a lot of appreciation for those hustling a livelihood or donating their time for work on stuff like this. Not to mention being humbled by trying to build something children can’t destroy over even just a three day period.
