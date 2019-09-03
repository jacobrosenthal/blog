+++
date = 2012-06-25T19:15:02.000Z
title = "Goertzel Arduino Library"
draft = false
in_search_index = true
aliases = ["/post/25868921072/goertzel-arduino-library", "/post/goertzel-arduino-library"]
[taxonomies]
tags = ["text"]
+++

For my ongoing Arduino watch project, we want to be able to do frequency detection in order to blink an led to bass hits.

There are a few Fast Fourier Transforms that have been written on Arduino including [this one](http://www.arduino.cc/cgi-bin/yabb2/YaBB.pl?num=1286718155 ) and [this one](http://elm-chan.org/works/akilcd/report_e.html). However, I needed my library to run on 8mhz clock along with whatever sampling rate change that would introduce. All the libraries I found were extremely optimized or poorly written with no abstraction so that I found it easier to start from scratch than attempt to use them.

So I set about figuring out how to implement something myself. I quickly learned about something called the Goertzel algorithm for when you actually only need to find a single frequency, vs a whole range, allowing all the savings you would expect from that. I found a few generic implementations of that as well on [wikipedia](http://en.wikipedia.org/wiki/Goertzel_algorithm) and [EEtimes](http://www.eetimes.com/design/embedded/4024443/The-Goertzel-Algorithm) but nothing specifically for Arduino. I tried implementing the generalized version on wikipedia but had lots of trouble with datatypes and my ability to properly debug on Arduino hardware. The EE times implementation's link was broken but some google-fu found it the [demo code](http://www.eetimes.com/Content/SourceCode/09banks.txt). It was written in C that I could compile on my laptop and get sane results. Then I could move it to Arduino slowly while maintaining those sane results. With this method I was able to keep everything working as I transitioned the code to a full [Goertzel Arduino library](https://github.com/jacobrosenthal/Goertzel).

I'm looking for feedback on how it should be implemented. Should it do the sample, or work on your existing array of samples? Is there an easier way to expose N and target frequency, perhaps some calculation or default? Let me know!
