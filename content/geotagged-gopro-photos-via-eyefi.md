+++
date = 2012-11-05T03:22:13.000Z
title = "Geotagged GoPro photos via EyeFi"
draft = false
in_search_index = true
aliases = ["/post/35033893129/geotagged-gopro-photos-via-eyefi", "/post/geotagged-gopro-photos-via-eyefi"]
[taxonomies]
tags = ["text"]
+++

![image](/images/tumblr_inline_p1w45xDCbd1rp3p4d_540.png)

TLDR; 

We now have geotagged photos and our uploads occur automatically at the end of the day via ftp! Thanks EyeFi!

<!-- more -->

I bought the new EyeFI pro x2 today mainly because it supports FTP and wifi geotagging. We figured we might be able to get some of these features 'free' without designing them into our board right this minute.  


Ideally it would be fun to have live shots of us as we go through our day, a lot like our hackerspace cam were you can see whats up with everyone at the lab.

In our testing it still takes at least 30 seconds and often more like 45 to get a single shot uploaded. I've found I can upload 0-3 photos within a minute depending on network congestion. However, the EyeFI does successfully get SSID data for geotag within our usual ~8 seconds on period! Note: The geo tagging happens at the server side where they appear to use skyhook. They add your GPS exif data and send it on to whatever service you've configured, ftp, flickr,etc. so you have to 'upload' it to get the exif data.

We want to avoid being on more than a minute, because the GoPro will take another photo because its intervalometer mode were (which takes a photo a max of once every 60 sec when you turn the camera on-- we just turn it off) 

The next problem is we would have to be on wifi at all times. Sadly the EyeFI uploads OLDEST first, which means if we miss an upload window we'll get further and further behind in our uploading. If we could get the EyeFI to upload the NEWEST we could sidestep that issue until charge time.

One option to maintain wifi all day is tethering to a data plan, but we're looking at 1.5GB data a day generally. I'm already a heavy data user getting throttled so that probably won't work. Ideally it would be best if we could upload thumbnails throughout the day and do a full dump at night, but again not an option with the EyeFI, nor does the GoPro generate thumbnails (except maybe in exif data?). There are other EyeFI style cards nowadays. Specifically we're looking into the FLU card which runs some kind of embedded linux with scripts, perhaps we can control more there? 

But for now, were just going save to the EyeFI all day (probably with some battery hit while it scans for SSIDs) and at the end of the day plug the card into the pc allowing uploads and tagging to occur all night while we sleep (though limiting our ability to cam our sleep).
