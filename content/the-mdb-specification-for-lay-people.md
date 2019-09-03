+++
date = 2011-10-08T00:41:00.000Z
title = "The MDB Specification for lay people"
draft = false
in_search_index = true
aliases = ["/post/22556477823/the-mdb-specification-for-lay-people", "/post/the-mdb-specification-for-lay-people"]
[taxonomies]
tags = ["mdb", "vending", "text"]
+++

I'm mainly working off of the specifications document by the NAMA people located at <http://www.vending.org/technology/MDB_Version_4-1.pdf>

Pinout:

GRN 6 MCommon 3 NC 

RED 5 MTX 2 0DC BRN

BLK 4 MRX 1 34DC WHT

Serial Communications:

9600 

1 start bit, 8 bits data, 1 mode bit, 1 check bit, 1 stop bit

check bit

  * drop carry byte, address+all data bytes.
  * A checksum will not be performed on ACK, NAK, or RET bytes.



mode bit-

  * from vmc sets if byte is address
  * from slave if last byte of data (or finished talking to master?)



transmit nrz

receive inverted

Misc:

"Each peripheral should be polled every 25-200 milliseconds. This can be done by

the POLL command or any other appropriate command."

Mtx need to source 100ma in order to drive optos!

Connectors:

Vertical Header: Molex 39-28-1063 ~1.25 on digikey

Right Angle Header: Molex 39-30-1060 ~1.25 on digikey
