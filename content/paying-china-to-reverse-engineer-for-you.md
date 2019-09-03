+++
date = 2017-11-23T04:07:07.000Z
title = "Paying China to reverse engineer for you"
draft = false
in_search_index = true
aliases = ["/post/167790047262/paying-china-to-reverse-engineer-for-you", "/post/paying-china-to-reverse-engineer-for-you"]
[taxonomies]
tags = ["text"]
+++

![image](/images/tumblr_inline_p1w3tj2wSz1rp3p4d_540.jpg)

In 2016 while visiting Shenzhen factories for a client, I wanted to hunt the markets for my favorite toys, dumb wearables, in order to learn from the design and see what parts are common and cheap. I bought everything I could until I found these veryfit id101′s I liked.   


<!-- more -->![image](/images/tumblr_inline_ozdw1bQHiS1rp3p4d_540.jpg)

  


![image](/images/tumblr_inline_ozdw41O9MC1rp3p4d_540.jpg)

The id101 have a [Nordic nrf51](https://www.nordicsemi.com/Products/nRF51-Series-SoC) bluetooth chip which is what I use in my work, and which has two open source bluetooth stacks, [Apache Mynewt](https://mynewt.apache.org) and [Zephyr](https://www.zephyrproject.org).

![image](/images/tumblr_inline_ozdw2ib9Xz1rp3p4d_540.jpg)

After charming my market contact by returning every few days to buy a handful more of them off her, I finally got back to a factory contact on WeChat. They’re made by [idoosmart](http://www.idoosmart.com/index.html) and they agreed to a tour of the factory. I was quite impressed with what I saw. They were clean and had complete testing throughout including water pressure testing every unit as far as I could tell. These guys put out roughly 10k per line per day, and they had several full lines running. I got quotes for something like $9 bucks with no heartrate, and $12 bucks with heartrate in quantities as low as 100. I was paying ~$20 in the markets, and a year later now the id101 can be bought for $20-$40 from [any one of many amazon resellers](https://www.amazon.com/s/ref=nb_sb_noss?url=search-alias%3Dsporting&field-keywords=id+101).  


I grabbed one of the cheap USB oscilloscopes in the markets and sat at Gee Coffee Roasters to reverse engineer my board. I desoldered all the components and took a picture to mark up while I probed the board.  


![image](/images/tumblr_inline_ozdwf4DZ6O1rp3p4d_540.png)

It wasn’t pretty but got the job done. I identified most of the components and connections.

  * Printed on board: “id101 ver 2.1 2016.06.13 3716″  

  * Nordic nrf51822 qfaca1 1609ab - Bluetooth LE  

  * hnox ver 2.2 2016.4.19 - HR sensor  

  * Azoteq iqs263a - Captouch Controller  

  * na45e - Battery charge or voltage regulator (?)  

  * "8c630 og155r" sot-23-8? - Erm driver (?)   

  * “2 w6 358411p ba 6" (15pin flex ribbon cable to SSD1306 oled  

  * "1187-02 hxs 2016.09" - 4pin Digitizer 4  

  * "ib 122" LGA-12? maybe Bosch Bma250e accelerometer (?)  




Durning this time I finally met Ian and Jin from [Dangerous Prototypes](http://dangerousprototypes.com/) who told me about their little known [Chinese reverse engineering](http://dangerousprototypes.com/store/reverse_engineering) service. For $80 they’ll reverse engineer a populated 2 layer PCB to Protel in a few days. I handed over $80 and a freshly purchased id101. After a few days Jin got back to me and said it was taking a bit longer. I forgot about it and a few weeks later I had a zip file with some nice pics of a 4 layer (oops) board which presumably slowed them down.  


![image](/images/tumblr_inline_ozdxy8ETVb1rp3p4d_540.jpg)![image](/images/tumblr_inline_ozdxymCnTb1rp3p4d_540.jpg)![image](/images/tumblr_inline_ozdxyu3ZPP1rp3p4d_540.jpg)![image](/images/tumblr_inline_ozdxz777Hk1rp3p4d_540.jpg)

The zip also had the the Protel CAD files. Protel was apparently bought by Altium and is now subsumed into their ~$10k designer tool. I tried to obtain an old copy to run in a VM but it ended up being a huge pain in the ass and so I got bored and put this project down.  


Recently, I found out that Altium’s free (though otherwise uncompetitive) online design tool [Circuitmaker](https://circuitmaker.com) will actually import Protel files including PCBS. I opened that old zip file in there and found it looking pretty good!   


![image](/images/tumblr_inline_ozdwkiJgrA1rp3p4d_540.png)

It probably took me a day or two of stitching screenshots, probing nets and marking up images in order to get my jpg. My working rate aside, $80 to get a fully interactive view of the board is worth it in every case I can think of.  


Sadly, thats about where I left the id101 project. [Find the id101 uploaded to my Circuitmaker account ](https://circuitmaker.com/Projects/Details/Jacob-Rosenthal/id101)with the zipfile as an attachment. Something I’d love to try next would be to try to actually produce a device based on reverse engineered files.  

