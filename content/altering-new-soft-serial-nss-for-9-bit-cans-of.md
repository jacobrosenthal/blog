+++
date = 2011-10-25T00:41:00.000Z
title = "Altering New Soft Serial NSS for 9 bit- cans of open source worms"
draft = false
in_search_index = true
aliases = ["/post/22556427458/altering-new-soft-serial-nss-for-9-bit-cans-of", "/post/altering-new-soft-serial-nss-for-9-bit-cans-of"]
[taxonomies]
tags = ["arduino", "vending", "text"]
+++

It looked like I should just be able to alter newsoftserial.cpp and newsoftserial.h  to take a uint_16 instead of 8, and then just step over 9 bits instead of 8 and I should have a pretty simple solution for RX.

<!-- more --> 

My first problem is NSS sadly virtualizes print so need to break stock install in order to move forward. I don't like it but for now I'm going to continue. I can alter hardwareserial.h and print.h to take the uint_16 as well and I'm good.

Another problem I found was NSS doesn't seem to properly (or fully?) implement print.  Neither dec, hex, bin are working to get raw data out, its always ascii format.  In researching I've found .write will do binary in both the print library, and nss, but nss has it marked private.  Found a forum post on adafruit where the writer of NSS claimed he was making .write public 3 years ago. Hah.

I believe I've come up with an elegant change to the NSS code to step over an arbitrary number of bits, making the code eventually able to support up to 16 bit serial if you'd want to. In the original code they simply shift left a binary 1 and use that as the mask for the bit to write, eventually shifting the 1 off the 8 bit number exiting the loop. 

>     for (byte mask = 0x01; mask; mask <<= 1) 
> 
>     {
> 
>       if (b & mask) // choose bit
> 
>         tx_pin_write(LOW); // send 1
> 
>       else
> 
>         tx_pin_write(HIGH); // send 0
> 
>       tunedDelay(_tx_delay);
> 
>     }
> 
>     tx_pin_write(LOW); // restore pin to natural state

I decided with a small change I could create a definable mask which could fit in this system

>   uint16_t limit = 0x200; // 9 would be x200, 10 would be x400 
> 
>     for (uint16_t mask = 0x0001; mask<limit; mask <<= 1)
> 
>     {
> 
>       if (b & mask) // choose bit
> 
>         tx_pin_write(LOW); // send 1
> 
>       else
> 
>         tx_pin_write(HIGH); // send 0
> 
>       tunedDelay(_tx_delay);
> 
>     }
> 
>     tx_pin_write(LOW); // restore pin to natural state

So, does it work?  I pulled out my trusty 

[Bus Pirate v2go](http://dangerousprototypes.com/bus-pirate-manual/)

(a must have) and was able to send some data over and confirm! Interesting note, despite my upgrading to the newest version which the version notes claimed to support 9 bit, the but pirate can't actually read a 9 bit, i just drops the MSB...  I made support forum post but so far nothing. I pulled the existing vending machine's line off and pipe it into arduino and was able to receive packets which when decoded made sense: 

> B 0000 1011  CHANGER  POLL B 0000 1011  CHANGER B 0000 1011  CHANGER B 0000 1011  CHANGER B 0000 1011  CHANGER B 0000 1011  CHANGER B 0000 1011  CHANGER B 0000 1011  CHANGER B 0000 1011  CHANGER 12 0001 0010 cashless device? POLL 12 0001 0010 cashless device? 12 0001 0010 cashless device? 12 0001 0010 cashless device? 12 0001 0010 cashless device? 12 0001 0010 cashless device? 34 0011 0100 bill validator 0 ACK to Bill Validator? 0 0 0 34 0011 0100 bill validator 34 0011 0100 bill validator 0 0 0 0 34 0011 0100 bill validator 34 0011 0100 bill validator 0 0 0 0 34 0011 0100 bill validator C 0000 1100 Changer 0 ACK F 0000 1111  CHANGER 0 Ack F 0000 1111  CHANGER 2A 0010 1010 energy mgmt ?? B 0000 1011  CHANGER B 0000 1011  CHANGER B 0000 1011  CHANGER B 0000 1011  CHANGER B 0000 1011  CHANGER B 0000 1011  CHANGER 
