---
title: "Running the LG Ultrafine 5k on Windows 10 & Linux"
layout: post
date: 2017-06-01 08:32
tag:
image:
headerImage: true
projects: true
hidden: false # don't count this post in blog pagination
description: "Thunderbolt 3 Monitor with Windows 10"
jemoji:
author: shantanujoshi
externalLink: false
---


<h2 id="heading2"> TL;DR</h2>
You can drive the LG Ultrafine 5k in W10 using a Thunderbolt 3 AIC (AsRock one ATM is the only one I tested) and a motherboard with the Thunderbolt 3 header on it.

<hr />

When the LG Ultrafine 5k was launched it was explcitily "built for mac" where there was no indication of compatibility with Windows devices. In fact, after its release, Linus@Linus Tech Tips in a review explained that Apple was using a special magical implementation of Thunderbolt 3 (TB3) where two displayport 1.4 signals were transmitted via the single TB3 cable making it impossible for non OSX devices with this implementation to use the 5k display at all. In fact after testing most people with TB3 laptops were only able to drive the display at 4K(4096x2160).

<h2 id="heading2"> WHO CARES BRUH JUST USE YOUR MACBOOK</h2>
Is what most people would say, but its important to note that this 5k screen is far ahead of any other 5k screen in this space. It destroys the Dell 5k screen in price, color representation, and brightness. This translates to stellar performance on the productivity front. I was determined to get this goddamn display working with some flavor of linux, but step 1 was windows 10.

<hr />

After some research into the TB3 spec, various motherboard manufacturers, and random tech blogs I learned the following:
<ol>
<li>You can't just plug in a DisplayPort to Thunderbolt 3 cable to power this from amazon because they aren't bidirectional and only convert TB3 to DP</li>
<li>The dual signal DisplayPort is NOT an Apple specific innovation it's in the TB3 specification</li>
<li>TB3 can use up to 8 lanes of DisplayPort 1.2 where as a normal connection uses 4 </li>
<li>Most motherboard manufacturers providing onboard TB3 aren't even providing a single DisplayPort signal for integrated graphics</li>
<li>The only way to pass through the GPU output is to use an AIC (add in card) that can support the TB3 spec AND passthrough graphics</li>
</ol>

<h2 id="heading2">Seems simple right?!</h2>
Sure if you can find a mobo and AIC... which turned out to be quite difficult. After a few hours of searching I was only able to find ONE AIC that was supported: [AsRock Thunderbolt 3 AIC](https://www.newegg.com/Product/Product.aspx?Item=N82E16815548003) and amazingly in its [manual](ftp://asrock.cn/Manual/Thunderbolt%203%20AIC.pdf) it even explicitly states support for 5k@60hz


I HAD to test this so I went ahead and purchased (referencing the manual) a compatible Z270 board and the AIC. I went with the AsRock Z270 Extreme4 (since it was mATX) and the AsRock AIC from newegg.


After throwing in my 960 pro, a titan XP, a single dim, and a 6700k, I plugged in the AIC with a special thunderbolt cable that inserts into a header on the motherboard. My guess here is that while the TB3 card is attached via PCIe the chipset also probably communicates with the AIC in some way for bandwidth allocation which is why that extra TB3 header is needed. The AIC failed to work on a motherboard without the special TB3 header.


I booted this system into windows 10, installed a TB3 driver from the AsRock website, and shutdown the system. I decided to plug in both of the two included cables (DisplayPort to DisplayPort and DisplayPort to Mini-Displayport) into the AIC. The logic here is that the single DP cable is restricted to 4K and in order to push the dual signal through TB3 I'd obviously need to attach two cables from the GPU to the AIC.

I plugged everything in, booted the system, and BOOM FULL 5k RESOLUTION 60HZ NO TINKERING!

The whole system works seamleslly and I've had no issues so far. Getting the full 10bit color support and the colors look fantastic. The speakers are still not cooperating (although my macbook running W10 can drive them no problem). I've got a hefty overclock on the Titan XP and was able to run GTA V at 5k at an average of 65 frames.

After installing TB3 drivers for arch I'm able to get this to run on arch linux as well so that's yuugeee. Gnome is pretty good at display scaling and I use Atom so both do well on the HiDPI screen. The TB3 driver is an intel driver so I think if your distro has Tb3 drivers floating around this may work. Shoot me an email if there's a distro you want me to test I'd be happy to give it a shot.  

<h2 id="heading2"> TL;DR</h2>
You can drive the LG Ultrafine 5k in W10 using a Thunderbolt 3 AIC (AsRock one ATM is the only one I tested) and a motherboard with the Thunderbolt 3 header on it.
