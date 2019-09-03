+++
date = 2015-05-01T07:00:00.000Z
title = "Parallax IDE for Chrome"
draft = false
in_search_index = true
aliases = ["/post/170847195187/parallax-ide-for-chrome", "/post/parallax-ide-for-chrome"]
[taxonomies]
tags = ["text"]
+++

![](/images/tumblr_inline_p43zzfWTJy1rp3p4d_540.jpg)

Im excited to announce that [Iced Dev](https://www.iceddev.com) and myself shipped a product I've been consulting on over the past few months, the [Parallax IDE for Chrome](https://www.parallax.com/news/2015-04-07/basic-stamp-chrome-programming-tool-proves-itself-educational-customers-will-soon). This allows teachers in schools around the world to continue their Parallax Basic Stamp curriculim in a world of Chromebooks.  


Parallax has a history of open source all the way [down to their silicon](https://www.parallax.com/microcontrollers/propeller-1-open-source) so it was a no brainer to work on this project with them and release it all on [their github](https://github.com/parallaxinc/Parallax-IDE).  


For my part I was able to make some upstream fixes to serial apis and develop a pure js basic stamp bootloader allowing Basic Stamp programming from both node and the browser. I also got to play with emscripten to package their C 'compiler' for an end to end browser experience. I'm really proud of the Iced Dev team and Parallax so check it out in the [app store now](https://chrome.google.com/webstore/detail/parallax-ide/djbdelcnligmaaddjeenddjodmiaoffo?hl=en).
