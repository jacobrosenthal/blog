+++
date = 2011-10-18T00:00:00.000Z
title = "MDB - 9 bit serial research"
draft = false
in_search_index = true
aliases = ["/post/22556458095/mdb-9-bit-serial-research", "/post/mdb-9-bit-serial-research"]
[taxonomies]
tags = ["arduinio", "mdb", "vending", "text"]
+++

I've done some reasearch on arduino, atmel and 9 bit serial. Again my goal is to stay as much in the Open Source toolchain as possible so that I don't have to support any more than I have to, and so my result is as standardized as possible:

* The arduino serial can not handle 9 bit transactions. :(
* Atmel, however does support it. "1 start bit • 5,6,7,8,or9databits • no, even or odd parity bit • 1or2stopbits"
* Looking at the existing Atmel serial library it is sadly hardcoded to 8 bits.
* Theres a bitbang serial library for arduino called New Soft Serial. It does not do 9 bit either :(. It seems like it would be not too terribly difficult to alter that code though.

So my options are
* a fresh atmel library, which arduino people wouldn't look at.
* A fresh arduino hardware or software serial implementation which I may be able to get upstreamed to them,
* altering the existing NSS product and attempting to get that upstreamed.

For now I choose altering NSS as it will be the least path of resistance. Here goes nothing.
