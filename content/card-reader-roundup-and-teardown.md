+++
date = 2013-03-25T08:20:00.000Z
title = "Card Reader Roundup and Teardown"
draft = false
in_search_index = true
aliases = ["/post/46238995080/card-reader-roundup-and-teardown", "/post/card-reader-roundup-and-teardown"]
[taxonomies]
tags = ["text"]
+++

Recently for a client project I needed to read credit card data to an Arduino. It didn't seem like it would be too hard or expensive since square gives out readers by the handful for free. I was only mildly familiar with the technology so I turned to [wikipedia](http://en.wikipedia.org/wiki/Magnetic_stripe_card) who told me the data is stored on Looks like track 1, format b.

A quick search on Sparkfun for an existing solution found their offerings to be HUGE and expensive! We wanted to embed some solution in a phone size package. Why is square able to make them so small and give them out free? Thus began my journey to destroy every card reader out there.

**SQUARE**

![image](/images/tumblr_inline_pk03jeZmMr1rp3p4d_540.jpg)

<!-- more -->

First a little googling led to a [teardown of the original square reader](http://www.northstreetlabs.org/squareup.html). I still tore mine apart anyway and found the same thing they found. The reader is literally a tapehead positioned perfectly to hit track 1, nothing more! Not even an amp!  Basically they did as much in software as they possibly could. Good job!

We wouldn't be using a phone jack in our solution and wouldn't have much processing power for cleaning the signal, but we spent some time trying to amp the signal and read the data. The signal was clearly evident and ampable, but our timeline didn't include reinventing card readers.

Much later in my research I actually found an [amazing talk from the Square engineers which explains everything](http://www.infoq.com/presentations/Android-Squared). Its a must watch.

In my research I found that Square had actually updated their model to add encryption. The update was touted for security, but I have trouble believing someone could man in the middle your headphone jack. A much more likely reason is using encryption to lock out the rise of the copycat mobile payment solutions like Intuit and Paypal. And of course to stop people like me from tracking down and repurposing handfuls of them.

![image](/images/tumblr_inline_pk03jfxTv91rp3p4d_540.jpg)

We surveyed our friends and found one of them in the wild to crack open. Sure enough theres now a coin cell battery and [TI micro](http://www.ti.com/product/msp430g2412) in there and the signal is nonsense.

**INTUIT** (circle)

![image](/images/tumblr_inline_pk03jfjAYO1rp3p4d_540.jpg)

The first Intuit reader I took apart was THEIR v1 as well.

![image](/images/tumblr_inline_pk03jfWZzR1rp3p4d_540.jpg)

It used a e42407bj from Magchip and a f1936 from Microchip that seemed to either be for encryption. Some digging from my partner Tim turned up a similar part at [IDTech](http://www.idtechproducts.com/products/component-accessories.html) that was very close to what we had which showed it actually output serial! Clearly they were simply in a rush to get to market and repurposed some existing silicon. Pricey for them, good for us.

I tried to locate more readers for cheap, but they were on their v2 now.

![image](/images/tumblr_inline_pk03jgsrpj1rp3p4d_540.jpg)

When I finally tracked one down and tore it apart they'd transitioned off the Magchip chip for a custom solution with encryption :(

![image](/images/tumblr_inline_pk03jgAfQL1rp3p4d_540.jpg)

![image](/images/tumblr_inline_pk03jhn3ft1rp3p4d_540.jpg)

So close!!!

**The PAYPAL**  (triangle)

![image](/images/tumblr_inline_pk03jh8hf41rp3p4d_540.jpg)

The Triangle is the most beautiful device of the bunch. The front cover is actually removable -- presumably for rebranding? The case, however, is impossible to get open. You can see my hacksaw damage in the photo above.

![image](/images/tumblr_inline_pk03jhxnRu1rp3p4d_540.jpg)

![image](/images/tumblr_inline_pk03ji3qH81rp3p4d_540.jpg)

Inside it looks a lot like these other second gen readers though with a ton more passive components. We've got a [8L151G ST Micro](http://www.mouser.com/ProductDetail/STMicroelectronics/STM8L151G6U6/?qs=RF4ygd%252bc9Xo71aXlmpKrVg==) and an [op amp package 6l04ste from Microchip](http://ww1.microchip.com/downloads/cn/DeviceDoc/cn544548.pdf). Presumably reading the signal and encrypting it for their app.

Again it makes this device not at all hackable and shows nobody going into this business at this point is going to leave their devices open any more.

**MAGTEK**

At this point Tim just looked up magchip readers and we found another company called Magtek. It turns out they actually have a [fully implemented chip and tape head solution that outputs RS232](http://www.magtek.com/V2/products/secure-card-reader-authenticators/43mm.asp). They're something like $15-25 in low qty which meant if we were doing anything other than a functional prototype they'd be no good, but they would fit our custom solution just fine. We were able to successfully implement the Magtek solution with no real problems and were very happy with the responsiveness. Sadly I didn't write the code, so if you want to see it please hassle [Tim](http://timgerrits.com/) into posting the code he wrote so you can benefit from our work too!
