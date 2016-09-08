---
title: "Getting Pascal GPU's to Work on Linux"
layout: post
date: 2016-09-04 21:08
tag: linux
image: 
headerImage: true
projects: false
blog: true
hidden: false # don't count this post in blog pagination
description: "Install Drivers on Linux"
jemoji: 
author: shantanujoshi
externalLink: false
---

I've been running ubuntu on computers with discrete GPU's for a few years now. Not ONCE has it ever been easy. The problem is that the Ubuntu default Nouveau drivers require time to update compatibility, and Nvidia drivers hate working with/disabling Nouveau. Given my itch to have the latest and greatest laptop hardware for the past few years I've had to deal with hacking away at the kernel/nouveau and nvidia beta drivers to get linux running on my various devices. Compatibility is generally introduced in kernel updates a couple months after the release of new hardware, but ain't nobody got time for that.

Around a month or so ago, after a friend at facebook gifted me an Oculus Rift; as a result I decided to build my own computer. I bought the new Nvidia GTX 1080 and a month later also purchased the new Pascal Titan X (or Titan XP, thanks linustechtips) and decided to dual boot Ubuntu 16.04 because I thought it'd be interesting to test CUDA benchmarks with the new GPU's. I also failed to find anyone post anything about their success or even failure with trying to run the GPU's on linux.

After hours of failure getting the beta linux drivers from BOTH the PPA and the official Nvidia website link to work with my install I finally found a method that I think works 100% of the time when getting Ubuntu to work with dGPUs.

<hr>
<h2> How to get new GPU's working with Ubuntu </h2>
Note: the following steps expect a fresh Ubuntu install. If you're trying to trouble shoot after installing, getting this to work would require at least being able to boot to TTY which may not be garunteed for certain installs. The basic framework is as follows:

<ol>
<li> Install ubuntu w/ the GPU unplugged or disable the PCIE for the GPU in BIOS </li>
<li> Boot into Ubuntu, run ALL updates, get the graphics PPA, and connect to the internet</li>
<li> Restart the computer to TTY </li>
<li> Purge Nurge nouveau and blacklist it just incase as well</li>
<li> Install latest nvidia release nvidia-###</li>
<li> Reboot, if it fails go back to tty and check .Xauthority permissions</li>
</ol>

These are the basics steps with some troubleshooting inbetween (nomodeset, permissions issues, grub issues). Detailed tutorial to follow.

