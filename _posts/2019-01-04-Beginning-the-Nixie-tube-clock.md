---
title: Beginning the Nixie tube clock
layout: post
published: true
tags: arduino nixie
---

So what the heck is a Nixie tube clock?  Or backing up a little, what the heck is a Nixie tube?  Today a Nixie tube is basically a retro-cool display device, but prior to the advent of the seven-segment LCD display, they were how you could go about displaying digital information on your device.  For example, a clock.  They look sorta like a mini neon light when lit up and I think are pretty cool.  I'd never seen nor heard of them before until a saw [one](https://millclock.com/nixie-clock/33-in-14-nixie-tube-clock-assembled-wood-enclosure-and-adapter-4-tubes) at a friends house.  I'd been thinking that I wanted a small project to work on using an Arduino, and so the idea was born: I'm going to build a Nixie tube clock.

Of course, I knew nothing about them.  Nor Arduino's for that matter.  As it turns out, Nixie tubes take a fair amount of voltage to drive them: 170V to light them up.  That's nothing to sneeze at.  I've zapped myself with 120V before and it was not pleasant, so 170V gives me a little bit of pause.

There are myriad ways to drive these things and if you're looking for the lowest cost, probably simplest solution, then EEVBlog has a 9-part Youtube playlist detailing how he [designed and built](https://www.youtube.com/watch?v=7uogKucrPks&list=PLvOlSehNtuHutdg1kZkG7aAYhjoJnk2fc) a Nixie tube display using some simple ICs.  Given that I'm also an electronics neophyte, I decided that I'd rather find something simpler which eventually led me to the exixe.

What's [exixe](https://www.tindie.com/products/dekuNukem/exixe-miniture-nixie-tube-driver-modules/)?  It's a little PCB that you can mount the Nixie tube to and which simplifies the development of a circuit to drive the tubes.  Using these boards I won't have to wire up a seemingly infinite number of ICs to drive all the tubes.  I picked up six of the IN-12 boards (my friends clock is using IN-14 tubes, so I wanted to be different) from tindie to use for my project.

I've been slowly accruing parts for this project but life keeps happening and getting in the way of actually _building_ it, but now that it's winter, it's time to make it a priority.  This is a list of few of the things I've acquired in persuit of this project (call it a BOM if you will):

* [Exixe boards](https://www.tindie.com/products/dekuNukem/exixe-miniture-nixie-tube-driver-modules/) 6x
* [Nixie tubes](https://ebay.us/niPtUu) 8x, since I wanted spares in case any go bad
* [Power supply](https://ebay.us/2gVIUq) I chose this particular supply since I'm planning on using an Arduino and it also has a 5V output to drive that with, in addition to the Nixie tubes from an adjustable 80-195V output
* [Socket pins](https://ebay.us/3xf7oy) These are probably unnecessary since you can solder the tubes directly to the exixe boards, but I like the idea of being able to plug/unplug the tubes to replace them.  The downside is that they're probably goingto compel me to have a much bulkier case for the finished clock than I otherwise would.
* [Arduino kit](https://www.amazon.com/dp/B01EWNUUUA/ref=cm_sw_r_tw_dp_U_x_lkrjCbQZQXTWW) I had pretty much no idea what exactly I'd need, so I just bought a full clone kit for the Mega which has a zillion IO pins.

So what are the next steps?  Well, I think there are a few things I need to figure out:

1. Time storage.  The kit includes an RTC module, so I think that's covered.
1. Setting the time.  I'm sure we've all seen clocks which are set by using an hour and a minute button.  Since I have six digits that means I'm looking at seconds as well, though I could probably save a button and assume that when the minute is set, the seconds are being set to zero.
1. But 6 digits is also good for showing MM/DD/YY display, so how do I set that?  I need a way to toggle into a date set mode also.
1. Or I could get an ESP8266 which has wifi and use that to drive everything and get time from NTP.
1. There's a thing called tube poisoning which basically renders some digits unusable.  This happens when a digit isn't used often enough (think of the 10's place in the hour slot, which will be either off, 1, or maybe 0 or 2 but 3-9 are basically never lit).  This is combatted by cycling through all the digits in the display.  I'll have to figure out the frequency this needs to be done at and how often it needs to happen.
1. How to deal with date display.  A button?  Flash it for a few seconds every minute?
1. A case.  Fun fact: I rationalized buying a 3d printer for this project :)  At some point I should probably blog about that as well.

I think the next post should be about learning to use the RTC and maybe getting some [code committed](https://github.com/ckattner/nixieclock).  I think for now I should probably use the LCD display from my kit for output before I start messing around with the tubes.
