+++
date = 2016-02-22T22:56:16.000Z
title = "Kicad to Advanced Circuits for PCBs and Assembly"
draft = false
in_search_index = true
aliases = ["/post/139813545072/kicad-to-advanced-circuits-for-pcbs-and-assembly", "/post/kicad-to-advanced-circuits-for-pcbs-and-assembly"]
[taxonomies]
tags = ["text"]
+++

Advanced circuits is a very high quality United States board house. They have a cheapish PCB service called [33each](http://www.4pcb.com/33-each-pcbs/) for small runs, though it generally doesn't compete with [OSHPark](https://oshpark.com/) if you ask me. Its only when you're doing a bunch of boards (~20-50) that they really shine. And, if you're doing boards through them, they offer assembly as well at frankly competitive prices to the DIY alternative [Small Batch Assembly](http://www.smallbatchassembly.com/).

<!-- more -->

You can choose as fast as 2 days, or 20 days with the cost on a sliding scale. For reference, my qty 50 ~1″x1″ nrf51 bluetooth boards were all told under 2k assembled in 5 days. Always check their [specials page](http://www.4pcb.com/4pcb-monthly-specials.html) to take a few hundred off your order, too.


For using Kicad for Design for Manufacture, you need to start with [this excellent post from Rheingold Heavy](https://rheingoldheavy.com/design-assembly-kicad/) which has inline responses from Small Batch.


Almost everything in that article is relevant from storing BOM data in eeschema elements, fiducials, to viewing gerbers in gerbview. We’ll talk about exceptions below.

For PCBs, sadly Kicad doesn’t have design rules (dru) like Eagle does. Advanced's standard (cheapest) board service, [lists tolerances](http://www.4pcb.com/pcb-design-specifications/) but remember these are all negotiable with a big board house like this! If you need tighter just talk to your rep and see if theres a cost.

So for a standard cheap board, with the inches icon on left on, click Design Rules->Design Rules and for all nets set:

* Clearance no less than .008″
* Track width no less than .008″
* Via diameters no less .020″
* Via drill no less than .010″ (ie a 5mil annular ring)

Another issue that wasn’t caught by FreeDFM initially was board edge clearance. There doesn’t appear to be a way to set this in Kicad, but you need to leave .015″ clearance of pads, vias, AND copper pours in order for them to separate your boards after manufacture and assembly. Make sure to move all your components an zones away from the edge, or just move your board edge back that much on all sides.

To generate the gerbers in pcbnew, click plot icon or File->Plot. [This Wayne and Layne post on Gerber generation](https://www.wayneandlayne.com/blog/2013/02/27/kicad-tutorial-gerber-file-generation/) was super helpful here.

* Layers, probably F.Cu (Top Copper), B.Cu(Bottom Copper) F.Paste(Top Solder Paste) F.Silk (Top Silkscreen), B.Silk (Bottom Silkscreen), B.Mask (Bottom soldermask), F.Mask (Top soldermask)
* Options, You might have other stuff checked, but the important one is to make sure Exclude PCB edge layer from other layers is unchecked as Advanced doesn’t take a separate edge cuts layer. Another nicety is check use auxiliary axis as origin so when you view in gerbview the file is in the center of the screen.
* Gerber Options, click Protel filename Options.
* Finally, Click Plot.

Now to generate the drill file, click Generate Drill File.

* Drill Units, use inches
* Zeros format suppress leading zeros
* Drill Map doesn’t matter
* Files options uncheck mirror y, use minimal header, and if you have non plated holes, Advanced takes a separate file for plated and non plated so make sure merge pth and npth holes into one file is unchecked.
* Drill Origin Auxiliary axis presuming you used "auxiliary axis as origin" in the plot screen.
* Finally, click Drill File then Close and Close and you Gerbers are in your project directory under GerberOutput

As the Rheingold article mentions, use gerbview to check your designs locally, then zip and upload them to [Advanced’s FreeDFM](http://www.freedfm.com) tool for further error and tolerance checking and tweak as needed.

One issue that wasn’t caught by FreeDFM was board edge clearance. There doesn’t appear to be a way to set this in Kicad(?), but you need to leave .015″ clearance of pads, vias, AND copper pours from board edges in order for them to separate your boards after manufacture and assembly. Make sure to move all your components an zones away from the edge, or just expand your board size that much on all sides.

Once your PCB is looking good, next you’ll need your BOM in excel format. Like in the Rheingold article, use BOM generation in eeschema. But what is different, you’ll need a grouped BOM layout (all like values and parts on same line). Luckily Kicad forum user Wolf wrote a Kicad BOM plugin for that, posted on the [Kicad forums as bom2groupedCsv](https://forum.kicad.info/t/bom-grouped-by-reference/261). But you’ll also need it converted to xlsx for your rep. so [I wrote a python script for that](https://gist.github.com/jacobrosenthal/99f506df5ca4cea7182a). Just run it with the only input the name of the BOM (by default is the name of the project no extension) ./csv2xls.py projectname

Finally you need your placement File-Fabrication Outputs->position (.pos). They call this a CPL file. Unlike in the article for for Small Batch Assembly you don’t need to change header names or merge any other BOM data on it, Advanced can pivot with the existing Ref, Val, and Package fields just fine. One note though, they don’t currently use the rotation data (Rot), so you need to have your pin1's marked nicely on your PCB silk! Finally, they'll take it columnar tab separated as it comes out of Kicad, so no need to format to xlsx or anything else for this one.


Finally, you have everything you need. Grab your final revision PCB quote number from FreeDFM, and [contact your regional rep via email](http://www.4pcb.com/Assembly-Specials.html) for an assembly quote. When they reply, also give them your xlsx BOM and .pos placement BOM. You might need to approve part substitutions, or if you’re stubborn, work to send them a reel of the parts you want used, but mostly Ive found if the part was well stocked on [Digikey](https://www.digikey.com/), Advanced would supply it for me.

Good Luck!

