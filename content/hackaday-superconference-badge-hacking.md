+++
date = 2017-11-15T21:43:17.000Z
title = "Hackaday Superconference Badge Hacking"
draft = false
in_search_index = true
aliases = ["/post/167530351112/hackaday-superconference-badge-hacking", "/post/hackaday-superconference-badge-hacking"]
[taxonomies]
tags = ["text"]
+++

![image](/images/tumblr_inline_p1w3efvbbV1rp3p4d_540.jpg)

At the [Hackaday](http://hackaday.io) [Superconference](https://hackaday.io/superconference/) this year [Blaine](https://github.com/phated) and I finally decided to try our hand at a conference badge puzzle. The cambadge was [introduced](https://hackaday.com/2017/10/11/building-the-hackaday-superconference-badge/) a month before the conference with the [source code](https://hackaday.com/2017/10/11/building-the-hackaday-superconference-badge/) following shortly after so you you could prepare hack ideas and even start prototyping shields and addons. In their words:

> It’s a camera. It has games, and it’s designed by [Mike Harrison] of Mike’s Electric Stuff. He designed and prototyped this badge in a single weekend. On board is a PIC32 microcontroller, an OV9650 camera module, and a bright, crisp 128×128 resolution color OLED display.

<!-- more -->

There would be prizes for best hardware hack, best app hack and even a film fest prize. But most importantly, there was also a puzzle prize. The puzzle firmware was implemented by [Mike Szczys](https://twitter.com/szczys?ref_src=twsrc%5Egoogle%7Ctwcamp%5Eserp%7Ctwgr%5Eauthor) with the ciphers being developed by [Jeff Rosowski](https://twitter.com/krux?lang=en) (Krux). 

Navigating to the puzzle menu revealed three options in binary, 00, 01, 10. 

![image](/images/tumblr_inline_ozfw4dQRg41rp3p4d_540.jpg)

00 was some graphical 'game', 01 appeared to be a reciting of the hacker's manifesto, and 10 was a ouija board. That's all the information we were given.  


  


## PUZZLE 00

![image](/images/tumblr_inline_ozfxzfHMpE1rp3p4d_540.jpg)

We halfheartedly played with the 00 puzzle while trying to be social during the pre party and started to put together a ruleset. A green cursor could be moved around an 8x8 grid by tilting the accelerometer. One button seemed to ‘place’ a red circle under the cursor. Further placements that shared a row (vertically, horizontally or diagonally) would light up the row in orange. 

![image](/images/tumblr_inline_ozfy1xEk2o1rp3p4d_540.jpg)

This was presumably a failure scenario but it was puzzling that we still had control of the cursor. A very jetlagged [Scotty from StrangeParts](https://www.youtube.com/channel/UCO8DQrSp5yEP937qNqTooOw) got six placements before giving it up and handing it back, suggesting to google it or write a script to solve it. We finally figured out the failure screen allows you to remove a failed placement and continue the game. This allowed us to put down a random six placements and continue taking back movements until we had all eight which went surprisingly quickly. In just a few minutes and roughly five take backs we had "Winner Winner!" printed on screen. 

![image](/images/tumblr_inline_ozfwp9GObF1rp3p4d_540.jpg)

Suspiciously, the menu screen also now has a set of hieroglyphic symbols under the 00 menu item. In googling later, we’d find out later this is a [Queens Puzzle](https://en.wikipedia.org/wiki/Eight_queens_puzzle) and we got a bit lucky. Theres 92 possible solutions but our methodology is called iterative repair and does not guarantee a solution.

  


## PUZZLE 10

![image](/images/tumblr_inline_ozfxb27lzf1rp3p4d_540.jpg)

We talked to [John Dahan](https://twitter.com/jedahan?lang=en) who won last year by using the strings command on the binary to find the success email to skip all puzzles. Strings is a common utility that prints all ascii characters it can find in a binary. We talked to Mike who said that wasn't going to work this year, but were were undeterred. Before even bothering to understand the puzzle ruleset we just started looking at the scrubbed source and production hex file. The source was definitely missing the puzzles, though we did get a dist folder with [intact elf](https://github.com/jacobrosenthal/cambadge/blob/master/dist/Normal/production/cambadge.X.production.elf) files. That could come in very handy and also means we don’t have to install MPLAB-X IDE ide to generate it myself. The .hex file was strange though. Generally .hex are [intel hex](https://en.wikipedia.org/wiki/Intel_HEX) format, ie ascii hex code representation with checksumming, but this was a binary. We wasted a bunch of time here remembering obj-copy stuff, only to realize we weren’t gaining anything and this was indeed a binary we could utilize as is. Running “strings Badge103.hex” output the results in [this gist](https://gist.github.com/jacobrosenthal/6c01f0d3fd309e6a3330d8623d35d812).  


After entering eight letters into ouija board the screen reads “What was that?” and appears to tell you which letters you had right by “X”ing out incorrect letters. 

![image](/images/tumblr_inline_ozfxc0yR7n1rp3p4d_540.jpg)

This would be super easy in retrospect, but hacking was way more fun. We searched the strings list for “What was that” hoping to find any suspicious text around it.  


 ****

> $ strings Badge103.hex  | grep -A 5 "What was that"
> 
> What was that?
> 
> HACKADAY  
> 
> MARKUSHESS
> 
> None
> 
> Not found
> 
> Read Err

HACKADAY is indeed eight characters which when entered was answered with “The planchette moves by itself:” and the code “PNIRHJZYL GSIXDF WFDNXJF JH CZDRI.”

![image](/images/tumblr_inline_ozfx6rTDef1rp3p4d_540.jpg)

Too lazy to bother cracking the cipher we entered “MARKUSHESS.” Though we still have no idea how to crack this code, Markus was the hacker from [Clifford Stoll’s The Cuckoo's Egg](https://en.wikipedia.org/wiki/The_Cuckoo%27s_Egg) so we weren’t surprised to receive an egg image.  


![image](/images/tumblr_inline_ozfxab0leg1rp3p4d_540.jpg)

We were subsequently kicked back out to the puzzle menu now with more symbols.  


![image](/images/tumblr_inline_ozh6y0gnf91rp3p4d_540.jpg)

##   


## PUZZLE 01

![image](/images/tumblr_inline_ozfxrxyAD11rp3p4d_540.jpg)

The puzzle consists of twenty-seven lines of the [Hacker’s Manifesto](https://en.wikipedia.org/wiki/Hacker_Manifesto) where you must scroll each line left or right to read it on the tiny screen. For some reason the cursor always starts at the fourth line which seems odd. At the bottom there is a list of twenty-seven negative and positive numbers with a four alpha character input to presumably complete the puzzle.

![image](/images/tumblr_inline_ozfxog9WHU1rp3p4d_540.jpg)

It seems obvious that the list of numbers maps to the lines of the manifesto. We looked to see if aligning the rows might spell a question in far right or left column that we could answer with four characters, but couldn't see anything obvious.  


![image](/images/tumblr_inline_ozfxt3c2AF1rp3p4d_540.jpg)

It was a huge pain to click buttons and invariably the badge would turn off or we’d get distracted and lose our place. We glanced through the strings dump for anything that might make sense for puzzle 10, but didn't see anything this time. As the party was ending we spent time running down mysterious QR codes that showed up around the venue thinking they could be related somehow, but were thrown out before we could get more than a few.   


![image](/images/tumblr_inline_ozfit0ixwv1rp3p4d_540.jpg)

Later we woudl find there was a (seperate) prize that unlocked on the badge if you scanned all ten of the mysterious QR codes sprinkled throughout the venues.

The next day we were bored looking at puzzles and wanted to do more reverse engineering. I've been looking for a reason to get better with Radare forever. [Radare](http://radare.org/r/) lets you snoop through binaries, disassemble them, rebuild the function graph, and even edit the code in place! So not unlike a [crackme](https://en.wikipedia.org/wiki/Crackme), we could presumably find the code that prints Winner, backtrace to find the branching instruction that decides success, and hardcode it to so that when we enter the game it gives us the winner screen. TLDR feel free to skip this section as we didn’t get anywhere, but we would love guidance to be better at this for the next conference.

  


## HUGE DIVERSION AHEAD

Radare has a bit of a learning curve, as described by a slide from a [recent talk](http://radare.org/get/r2avtokyo-en.pdf) from the founding developer, pancake.

![image](/images/tumblr_inline_ozfh097ZqW1rp3p4d_540.jpg)

We can open our binary file in Radare and analyze it for functions, printing the results.  


> $ r2 -a mips -e asm.bits=32 Badge103.hex 
> 
> WARNING: bin_strings buffer is too big (0x02bf8a80). Use -zzz or set bin.maxstrbuf (RABIN2_MAXSTRBUF) in r2 (rabin2)
> 
> \-- It's not a bug, it's a work in progress
> 
> [0x00000000]> aaa
> 
> [x] Analyze all flags starting with sym. and entry0 (aa)
> 
> [ ] 
> 
> [aav: Cannot find section at this address
> 
> aav: Cannot find section at this address
> 
> [x] Analyze len bytes of instructions for references (aar)
> 
> [x] Analyze function calls (aac)
> 
> [ ] [*] Use -AA or aaaa to perform additional experimental analysis.
> 
> [x] Constructing a function name for fcn.* and sym.func.* functions (aan))
> 
> [0x00000000]> afl
> 
> 0x00000000    1 16           fcn.00000000
> 
> [0x00000000]>

We should see a huge list of functions, but sadly we don’t. Earlier we found someone saved us having to install MPLAB-X IDE and we also have an [unmangled elf](https://github.com/jacobrosenthal/cambadge/blob/master/dist/Normal/production/cambadge.X.production.elf) to mess with.

> $ r2 -a mips ~/Downloads/cambadge.X/dist/Normal/production/cambadge.X.production.elf 
> 
> Warning: Cannot initialize dynamic strings
> 
> \-- The unix-like reverse engineering framework.
> 
> [0x9d009000]> aaa
> 
> [x] Analyze all flags starting with sym. and entry0 (aa)
> 
> [ ] 
> 
> [aav: using from to 0x9d000000 0x9d08b3f3
> 
> Using vmin 0x9d000000 and vmax 0xbfc00c00
> 
> aav: using from to 0x9d000000 0x9d08b3f3
> 
> Using vmin 0x9d000000 and vmax 0xbfc00c00
> 
> [x] Analyze len bytes of instructions for references (aar)
> 
> [x] Analyze function calls (aac)
> 
> [ ] [*] Use -AA or aaaa to perform additional experimental analysis.
> 
> [x] Constructing a function name for fcn.* and sym.func.* functions (aan))
> 
> 0x9d008180    1 16           sym._gen_exception
> 
> 0x9d008200   44 1384         sym.__vector_dispatch_0
> 
> 0x9d008220   43 1352         sym.__vector_dispatch_1
> 
> ….
> 
> 0x9d023cd8    1 8            sym._on_bootstrap
> 
> 0x9d023ce0    1 8            sym._libc_private_storage
> 
> 0xbfc00480    3 1908         sym.__DbgExecReturn
> 
> [0x9d009000]>

That’s what we’re supposed to see! We can even visualize a complete call graph.

![image](/images/tumblr_inline_ozfgpjXkfb1rp3p4d_540.png)

But remember, we know this has all our puzzles stripped so there won’t be much to see here. What we want is this view in our puzzle inclusive binary. Why doesn't our binary ‘hex’ file load cleanly into Radare? Presumably the elf file has a bunch of debug info like [sections and entry point (reset vector)](https://gist.github.com/jacobrosenthal/beb2573e55e07c8cb04101e6f45b42c1) to help set up Radare automatically which we don’t understand how to do manually. So how do we help it? In our production dist files we also have a [.map file](https://github.com/jacobrosenthal/cambadge/blob/master/dist/Normal/production/cambadge.X.production.map) that has the function names and addresses in it. There we find the [reset address](https://github.com/jacobrosenthal/cambadge/blob/master/dist/Normal/production/cambadge.X.production.map#L397)  


> .reset                  0x9d009000          0x1e4         484  Reset handler 

And from cambadge.X.production.elf we can get the entry point(reset vector) to confirm

> [0x9d009000]> ie
> 
> [Entrypoints]
> 
> vaddr=0x9d009000 paddr=0x00009000 baddr=0x9d000000 laddr=0x00000000 haddr=0x00000018 type=program
> 
> 1 entrypoints
> 
> [0x9d009000]>
> 
> And we can print the hexdump of the binary code at that location
> 
> [0x9d009000]> px @ 0x9d009000
> 
> \- offset -   0 1  2 3  4 5  6 7  8 9  A B  C D  E F  0123456789ABCDEF
> 
> 0x9d009000  0224 400f 0000 0000 0060 1a40 c004 5a7f  .$@......`.@..Z.
> 
> 0x9d009010  0500 4013 0000 0000 029d 1a3c a43c 5a27  ..@........<.<Z'
> 
> 0x9d009020  0800 4003 0000 0000 01a0 1d3c f0ff bd27  ..@........<...'
> 
> 0x9d009030  00a0 1c3c f07f 9c27 029d 083c d03c 0825  ...<...'...<.<.%
> 
> 0x9d009040  09f8 0001 0000 0000 00a0 083c 1c00 0825  ...........<...%
> 
> 0x9d009050  01a0 093c 5cea 2925 0600 0010 0000 0000  ...<\\.)%........
> 
> 0x9d009060  0000 00ad 0400 00ad 0800 00ad 0c00 00ad  ................
> 
> 0x9d009070  1000 0825 2b08 0901 f9ff 2014 0000 0000  ...%+..... .....
> 
> 0x9d009080  029d 083c f8fb 0825 0000 098d 1800 2011  ...<...%...... .
> 
> 0x9d009090  0400 0825 0000 0a8d 0400 0825 0000 0b8d  ...%.......%....
> 
> 0x9d0090a0  0900 6011 0400 0825 0000 0c91 ffff 4a25  ..`....%......J%
> 
> 0x9d0090b0  0100 0825 0000 2ca1 fbff 4015 0100 2925  ...%..,...@...)%
> 
> 0x9d0090c0  0500 0010 0000 0000 0000 20a1 ffff 4a25  .......... ...J%
> 
> 0x9d0090d0  fdff 4015 0100 2925 0300 0825 fcff 0a24  ..@...)%...%...$
> 
> 0x9d0090e0  2440 4801 0000 098d e7ff 2015 0000 0000  $@H....... .....
> 
> 0x9d0090f0  0000 093c 0000 2925 1000 2011 0000 0000  ...<..)%.. .....
> 
> [0x9d009000]>

Back to our puzzle inclusive binary code, Let’s search for that reset vector bytecode “0224 400f” as that shouldn't have changed even with puzzles stripped out:

> $ r2 -a mips -e asm.bits=32 Badge103.hex 
> 
> [0x00000000]> /x 0224 400f
> 
> Searching 3 bytes in [0x0-0x2bf8a80]
> 
> hits: 5
> 
> 0x00000e80 hit0_0 022440
> 
> 0x00006d66 hit0_1 022440
> 
> 0x000102ce hit0_2 022440
> 
> 0x000191fe hit0_3 022440
> 
> 0x00025466 hit0_4 022440
> 
> [0x00000000]> px @ hit0_0
> 
> \- offset -   0 1  2 3  4 5  6 7  8 9  A B  C D  E F  0123456789ABCDEF
> 
> 0x00000e80  0224 400f 0000 0000 0060 1a40 c004 5a7f  .$@......`.@..Z.
> 
> 0x00000e90  0500 4013 0000 0000 039d 1a3c 9cd6 5a27  ..@........<..Z'
> 
> 0x00000ea0  0800 4003 0000 0000 01a0 1d3c f0ff bd27  ..@........<...'
> 
> 0x00000eb0  00a0 1c3c f07f 9c27 039d 083c c8d6 0825  ...<...'...<...%
> 
> 0x00000ec0  09f8 0001 0000 0000 00a0 083c 3c00 0825  ...........<<..%
> 
> 0x00000ed0  01a0 093c b0ea 2925 0600 0010 0000 0000  ...<..)%........
> 
> 0x00000ee0  0000 00ad 0400 00ad 0800 00ad 0c00 00ad  ................
> 
> 0x00000ef0  1000 0825 2b08 0901 f9ff 2014 0000 0000  ...%+..... .....
> 
> 0x00000f00  029d 083c d478 0825 0000 098d 1800 2011  ...<.x.%...... .
> 
> 0x00000f10  0400 0825 0000 0a8d 0400 0825 0000 0b8d  ...%.......%....
> 
> 0x00000f20  0900 6011 0400 0825 0000 0c91 ffff 4a25  ..`....%......J%
> 
> 0x00000f30  0100 0825 0000 2ca1 fbff 4015 0100 2925  ...%..,...@...)%
> 
> 0x00000f40  0500 0010 0000 0000 0000 20a1 ffff 4a25  .......... ...J%
> 
> 0x00000f50  fdff 4015 0100 2925 0300 0825 fcff 0a24  ..@...)%...%...$
> 
> 0x00000f60  2440 4801 0000 098d e7ff 2015 0000 0000  $@H....... .....
> 
> 0x00000f70  0000 093c 0000 2925 1000 2011 0000 0000  ...<..)%.. .....
> 
> [0x00000000]>

Found it! Maybe we can shift our 0x00000e80 address by 0x9D008180 so it becomes 0x9d009000 and Radare has more success analyzing functions? This is where we gave up though. Anyone reading this please reach out if you can help us understand Radare better for the next conference.

  


## Back on track

A day lost, we went back to solving it the honest way -- sort of. Blaine wasn’t even an official attendee so we were having to share a badge. Since we were armed with the strings dump of the manifesto text and list of integes we turned to node to [script something](https://gist.github.com/jacobrosenthal/cf9d5ce5f15db817feb966970c33b007) to print the columns so we could maybe see what we couldn’t see with our own eyes.  


Still, nothing looked right and we went down a hundred other rabbit holes that didn't work out, all the while begging Krux and Mike for any guidance. Finally when the conference ceremony was just hours away Krux helped us find our script had an off by one error. With that fixed it turns out all this time a middle column read “[realbunniehuanghardwarehack](https://gist.github.com/jacobrosenthal/e33ce0826a0cda175ab3c749b16accf1#file-cambage-manifesto-out-L62)” Bunnie was perhaps first known for hacking the xbox. “Winner Winner!” 

  


## A Fourth Puzzle

![image](/images/tumblr_inline_ozfi5ykrTl1rp3p4d_540.jpg)

Now we had a third set of hieroglyphs and “[badge17@hackaday.com](mailto:badge17@hackaday.com)”. To be fair we saw this email in the strings earlier, so we're pretty sure we'd be seeing it again. But what were these glyphs?

Several, especially the last one sure looks like [unicode](http://www.charbase.com/2e2c-unicode-squared-four-dot-punctuation) but we couldn’t find many of the rest. We spent a lot of time on that before asking Krux who didn't seem interested in that line of reasoning. We decided to do a transposition arbitrarily to the english alphabet just to play with the characters. Transposing the first character to a, and so one, we got “abcde fgahidjkclefg gmgce ccgcm nkeopfi” There were only 16 distinct 'letters', with c, g, and e being highest in frequency. However this tiny subset of text just doesn't lend to any kind of [frequency analysis](https://en.wikipedia.org/wiki/Frequency_analysis). We spent a lot of time thinking the spaces were useful and that “ccgcm” would be an odd word with double repeated starting letter. Llama didn’t seem likely, but you never know. We looked at brute forcing rot, morse and other symbol alphabets but didn’t come up with anything that worked before we finally ran out of time.

During the badge ceremony one other team had apparently also got this far and was awarded some cash for their efforts. Mike and Krux spoiled the last puzzle on stage, it's apparently the [Commander Keen, Standard Galactic Alphabet](http://www.shikadi.net/keenwiki/Standard_Galactic_Alphabet). When translated it reads: “PRESTONPLUSWHEATONNINETEENEIGHTYFOUR” which is a [Last Starfighter](http://www.imdb.com/title/tt0087597/) reference. Presumably emailing “Last Starfighter” to [badge17@hackaday.com](mailto:badge17@hackaday.com) would have won us the that sweet $256 prize.

## Next time

Huge thanks to everyone involved at Superconference. It was a crazy lineup of amazing speakers. It was also awesome to see so much money given away to the Hackaday prize entrants I had been bumping into all weekend. Huge thanks to Mike and Krux for getting us to commit to a badge puzzle for the first time and for helping us through to the (very) end.

![image](/images/tumblr_inline_ozhayysWe31rp3p4d_540.jpg)
