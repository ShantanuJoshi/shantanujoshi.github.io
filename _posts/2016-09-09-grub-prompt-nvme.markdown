---
title: "Booting Into Linux from the Grub Prompt with an NVME Drive"
layout: post
date: 2016-09-09 00:15
tag: linux
image: 
headerImage: true
projects: false
blog: true
hidden: false # don't count this post in blog pagination
description: "Boot Linux from the Grub Prompt"
jemoji: 
author: shantanujoshi
externalLink: false
---

For the first time in my foray into Linux for the past few years now I ran into the dreaded grub prompt at boot. 

It looks a lot like this:
<img src="http://terminalinflection.com/wordpress/wp-content/uploads/2012/10/GRUB-Ubuntu.png">

This basically means that the grub install is corrupted and GRUB doesn't know how to boot.

There are quite a few tutorials on recovering from a grub, infact the image above includes most of the neccesary steps to booting into grub. But here's my experience recovering from this prompt with an NVME Pcie SSD. In my first attempt to follow the steps below I had a kernel panic and had to start from scractch because I followed the steps to a regular recovery.

<h2 id="heading2"> Steps to Recover from the Grub Prompt </h2>
Here's a step by step method to how I recovered from the grub prompt, fixed grub, and rebooted to write this post.

<strong>Part 1: Getting Out of the Grub Prompt</strong>

<ol>
<li>Type <strong><code><span class="evidence">ls</span></code></strong> to see which drives are mounted</li>
<li>Type <strong><code><span class="evidence">ls (hd0,1)/</span></code></strong> and repeat this until you find the drive <strong><code><span class="evidence">(hdX, Y)/</span></code></strong> with your boot disk </li>
<li>Once you've found your boot disk type: <strong><code><span class="evidence">set root=(hdX,X)</span></code></strong> where X is your drive/partition number </li>
<li>The next part depends on your version of Linux (but if you're after version 12 you're good so keep reading)</li>
<li>Type <strong><code><span class="evidence">linux /vmlinuz root=/dev/nvme0nXpY </span></code></strong> where X is the X from hdX which is your boot drive, and Y which is the partition number on that drive that the boot partition.</li>
<li>initrd /initrd.img</li>
<li>boot</li>
</ol>






<strong>Part 2: Booting into Linux and Repairing GRUB</strong>

After beginnning the boot process from the prompt I noticed a flickering TTY screen at boot due probably to my Nvidia drivers or some other permissions error. I knew to basically type <strong><code><span class="evidence">Ctrl + F1</span></code></strong> until I got get a TTY screen (which would disappear within 3 seconds due to the nature of this flickering bug, and could be brought back by pressing <strong><code><span class="evidence">Ctrl + F1</span></code></strong>) 

 

So while fighting with the flickering TTY screen I had to enter my username, password, and the command <strong><code><span class="evidence">sudo service GDM stop</span></code></strong>. This command may be: <strong><code><span class="evidence">sudo service lightdm stop</span></code></strong> if you have a different display manager.

Basically my display manager was in a corrupted loop because the .Xauthority file's permissions are altered either during the grub prompt boot. The permissions change to root effectively. As a result upon stopping the display manager I am able to access the TTY and preform the following steps:

<ol>
<li> Type the command <strong><code><span class="evidence">update-grub</span></code></strong> in the tty </li>
<li> You should see a series of images to add to the grub menu, next enter <strong><code><span class="evidence">grub-install /dev/nvme0nXpY</span></code></strong> as per your prior boot drive and partition</li>
<li> Now to check .Xauthority permissions, type <strong><code><span class="evidence">sudo ls -lah</span></code></strong> in your home directory to see what the permissions settings are for .Xauthority file. In my case this was "root:root"</li>
<li> To repair .Xauthority type the following replacing username with your username <strong><code><span class="evidence">chown username:username .Xauthority</span></code></strong> in my case I typed shantanu:shantanu </li>
<li> Type <strong><code><span class="evidence">sudo reboot</span></code></strong> and hope for the best </li>
</ol>

After this I waited for the grub screen and indeed it worked. The NVME0nXpY thing was neccesary for me to boot and subsequently type this post.