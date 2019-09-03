+++
date = 2013-03-27T19:56:37.000Z
title = "Lasering PCB enclosures"
draft = false
in_search_index = true
aliases = ["/post/46441281948/lasering-pcb-enclosures", "/post/lasering-pcb-enclosures"]
[taxonomies]
tags = ["text"]
+++

![image](/images/tumblr_inline_pk17wqRMIP1rp3p4d_540.jpg)

This week I used the laser to cut some holes in my enclosures to make way for switches, light pipes, etc. My previous attempts pre-hackerspace (with a dremel) were.. rough.

<!-- more --> 

![image](/images/tumblr_inline_pk17wqGy4k1rp3p4d_540.jpg)

There had to be a better way! The big problem with using the laser was jigging the case in the laser in such a way that I could reliably and repeatedly cut in the perfect spot. After a few attempts I found a solution.

![image](/images/tumblr_inline_pk17wq7SDX1rp3p4d_540.png)

First I exported my front board dimension and mill holes from Eagle using run -> dxf.ulp, opened it in our laser program, mirrored it and adjusted some holes and sizes.

![image](/images/tumblr_inline_pk17wrHN4u1rp3p4d_540.jpg)

I grabbed a square piece of stock and dropped up the in the upper corner of the laser and homed the laser head. Now, by lasering that outline on my stock, I can take it out of the machine and put it back in the same place every time.

![image](/images/tumblr_inline_pk17wr8WG41rp3p4d_540.jpg)

I can also match the PCB up over the top of the etch.

![image](/images/tumblr_inline_pk17wsUk3h1rp3p4d_540.jpg)

And, finally, since the PCB is designed to fit the case perfectly, I can just drop the case on top of the PCB.

![image](/images/tumblr_inline_pk17wsx6MI1rp3p4d_540.jpg)

Wonderful. I could still use a method to cut cleaner on the other 4 sides, but for now Im happy doing a little bit of clean up work and having my cuts be entirely though the case.
