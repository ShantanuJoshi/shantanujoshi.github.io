---
title: "Modding an AIO Water Cooler for the Titan XP (Pascal)"
layout: post
date: 2016-09-02 18:21
tag: hardware
image: 
headerImage: true
projects: true
hidden: false # don't count this post in blog pagination
description: "Titan X AIO Water Cooler"
author: shantanujoshi
externalLink: false
---

 

I recently got my hands on a new Pascal Titan X, and while the performance of the card is phenomenal it has terrible idle and load temps. In this post I'll describe my steps in modding a hybrid water cooling kit that's fit for the GTX 1080 to work with the new Titan X. <em>Scroll down to skip to the tutorial</em> 



{% include image.html
        	img="assets/images/TitanXPMod/1.JPG"
            title="Titan XP"
            caption="Titan XP" %}

<h2> Why water cool? </h2>

Nvidia's default blower-style coolers are relatively inefficient, and unfortunately AIB's (Add-in Board Partners) are not allowed to release custom cooling solutions or modify the reference PCB Nvidia creates for the Titan series.  

 

As a result the only solution to better performance and temperatures is water cooling. There is a large community of PC enthusiasts that build custom water cooling loops for their systems. Unfortunately custom loops are expensive and cumbersome. In addition they tend to make upgrading quite difficult. The next solution to water cooling a graphics card is a "hybrid-kit". Basically an all in one water cooler that attaches to the GPU PCB and creates a water cooling loop. 

 

EVGA (an AIB that releases custom loops) does not have a water cooling kit for the new Titan X. The only option is to modify a water cooling kit made for the Titan X's younger brother the GTX 1080.  

 

{% include image.html
        	img="assets/images/TitanXPMod/2.JPG"
            title="EVGA Hybrid"
            caption="EVGA 1080 Hybrid Kit" %}
 

<h2> How to Mod the EVGA 1080 Hybrid Kit for the Titan X </h2> 

Installing the kit with or without mods first requires complete removal of the original cooler from the graphics card.

<em>Warning: this will void your warranty with nvidia, but if you put the original cooler back on there's no way for them to know you've removed it. I'm not saying I recommend doing so but I'm also saying there are no tamper-proof screws...</em> 

 
<strong>Note before continuing:</strong>
<ul>
<li>Keep careful track of all the screws, you'll need them in the future </li>
<li>Try to find a dremel tool, if you don't have one it's a perfect opportunity to pick one up, I'll specify the attachment bits used in each step</li>
<li>If you're afraid or unsure of removing the GPU cooler from the PCB I recommend watching this <a href="https://www.youtube.com/watch?v=H7HN3CDxMQk">video</a> detailing the teardown of the Titan X</li>
<li>You must ground yourself somehow while doing this. Click <a href="https://www.tomshardware.com/faq/id-2121341/ground-building-computer.html">here</a> to learn why it's necessary</li>
</ul>

 

<h2>Step 1: Remove the IO Plate</h2>

Start by removing the 5 screws on the IO plate, the two screws for the DVI port, and the two screws on the back plate holding the IO plate in place. 

 


{% include image.html
        	img="assets/images/TitanXPMod/3.JPG"
            title="Titan X IO Plate"
            caption="Remove this IO Plate" %}
 

 

<h2>Step 2: Unscrew the Cooler</h2>

Get yourself two allan/hex keys/bit, a tiny phillips 00, and a larger philips head. I didn't take pictures of the cooler removal given that there's no real trick here. Here's the best order of operations for the removal: 
<ol>
<li>Remove the back plate by carefully unscrewing the TINY screws holding it in place (one part of the backplate slides out of the other)</li>
{% include image.html
            img="assets/images/TitanXPMod/backplategone.JPG"
            title="Backplate Removed"
            caption="Backplate Removed" %}

<li>Use the smaller allan key to remove all the screws surrounding the cooler, the four larger screws next to the clear window are only there to hold the window to the plate itself (see photo of larger screws)</li>
</ol>


{% include image.html
        	img="assets/images/TitanXPMod/4.JPG"
            title="Titan X Cooler Screws"
            caption="Remove all but the optional circled screws" %}
 


<h2>Step 3: Remove the Cooler</h2> 

Again I didn't think this step needed documentation. The best way to do it is remove the section with the window first, you will experience some resistance from the thermal compound on the heatsink but ignore it. Next remove the second cooler, be careful of the wire connecting the fan to the PCB and remove it carefully. Once the entire cooler is removed and you've wiped the GPU surface with a microfiber cloth dipped in some alcohol... 

Watch out for these wires when removing the two parts of the cooler
<div class="side-by-side">
    <div class="toleft">
        <p><img class="image" src="/assets/images/TitanXPMod/blowerfanwire.JPG"></p>
    </div>
    <div class="toright">
        <p><img class="image" src="/assets/images/TitanXPMod/ledwire.JPG"></p>
    </div>
</div>


It should look something like this: 
 

{% include image.html
        	img="assets/images/TitanXPMod/5.JPG"
            title="Titan X PCB"
            caption="Nvidia GP102" %}

<h2>Step 4: Modifications to the EVGA Kit</h2> 

The evga kit consists of 3 major parts: the AIO water cooler, a pcb plate, and a top cover. The AIO cooler fits onto the GPU perfectly as both the Titan X and the 1080 use the GP102 chip, the only issue is mounting the PCB plate with the fan onto the Titan X PCB. The plate needs to accommodate for the following features of the Titan X:
<ol>
<li> Extra Capacitors</li>
<li> S6-pin power connector </li>
<li> Additional Phase Chip </li>
</ol>
 

{% include image.html
        	img="assets/images/TitanXPMod/6.JPG"
            title="Additional PCB Items"
            caption="Additional Titan X Components" %}
 

<h2>Step 5: Make Room for an Extra 6-Pin</h2> 

I started with this as it seemed the simplest, I used a cutting tool and eyeballed the additional cuts needed for the plate. The removed section is highlighted below: 

 

{% include image.html
        	img="assets/images/TitanXPMod/7.JPG"
            title="Space for 8+6Pin"
            caption="Area Removed for 6-Pin" %}
 

<h2>Step 6: Accomodating the Extra Phase Chip</h2> 

Cut out a section for the extra phase chip. This part is tricky, I started by using a cutting tool to cut out a square a bit smaller than the area I thought I needed (all eyeballed). After which I brought the plate close to the PCB to see how much more metal I would have to remove and used a grinding bit to cut away slowly at the plate. 

 

Here are my results: 


{% include image.html
        	img="assets/images/TitanXPMod/8.JPG"
            title="Cuts for Phase Chip"
            caption="Area Removed for Extra Chip" %}
 
{% include image.html
        	img="assets/images/TitanXPMod/9.JPG"
            title="Larger View of Cuts"
            caption="Wider View of the Cut for Scale" %}
 

<h2>Step 7: Grinding a Space for the Capacitors</h2> 
This is the aftermath of the panel after I grinded away the metal above the capacitors. I highly recommend using a dremel with the following [bit](https://www.dremel.com/en-us/Tools/Pages/ToolDetail.aspx?pid=541). It's included in most sets and makes it very easy to grind the surface away.

{% include image.html
            img="assets/images/TitanXPMod/10.JPG"
            title="Side View of Dremel Cut"
            caption="Plenty of Space for the Capacitors" %}

{% include image.html
            img="assets/images/TitanXPMod/11.JPG"
            title="Slightly Zoomed Out"
            caption="Slight Collateral Dremel Damage on the Sides" %}
