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
<li> Install Ubuntu: to boot into the installer edit the boot parameters and add nomodeset before quiet splash</li>
<li> Boot into Ubuntu with nomodeset, run ALL updates and connect to the internet</li>
<li> (Optional) Restart the system, add nomodeset again, download the latest kernel and upgrade the kernel</li>
<li> Restart the computer, same setup with nomodeset, add the graphics PPA, then logout </li>
<li> Switch to TTY, login and stop the desktop envrionment service (gdm or lightdm depending on your OS)</li>
<li> Purge the nouveau driver</li>
<li> Install latest nvidia driver <strong><code><span class="evidence">nvidia-###</span></code></strong></li>
<li> Reboot to your OS</li>
</ol>

These are the basics steps detailed tutorial below.


<h2>0. Installing Ubuntu</h2>
The steps to installing ubuntu vary based off of your needs. In my case I generally skip the preset options for installation and click "something else" where I can add my own partition scheme. I prefer to create a partition for <strong><code><span class="evidence">/</span></code></strong> and <strong><code><span class="evidence">/home</span></code></strong> generally alloting 30-50 gigs for / and the rest for /home on the drive. My tutorial assumes you've got a live disk of your chosen distro (personall running Gnome 16.04 because the UI is fantastic).

<h2>1. Booting into the Live Disk</h2>
In order to boot into the live disk for the install you need to highlight the "Intall Ubuntu" option at the live disk grub menu and type <kbd>e</kbd> to edit the commands and add <strong><code><span class="evidence">nomodeset</span></code></strong> right after "quiet splash", I also recommend changing quiet splash to <strong><code><span class="evidence">noquiet nosplash</span></code></strong> but that's optional

<div class="side-by-side">
	<div class="toleft">
		<p><img class="image" src="http://www.tecmint.com/wp-content/uploads/2016/04/Ubuntu-16.04-Boot-Screen.png" alt="Alt Text"></p>
	</div>
	<div class="toright">
	<img class="image" src="https://www.maketecheasier.com/assets/uploads/2009/12/ubuntukarmic-edit-grub-entr.png" alt="Alt Text">
	</div>
</div>

<h2>2. Boot into Ubuntu</h2>
After the install you should see the regular grub menu, once the grub menu appears type "e" again to edit the boot commands and type nomodeset as in step 1. Nomodeset is neccesary at boot because it disables certain video drivers which may fail with newer GPU's. 

Once logged in, connect to the internet and open up a terminal window and run: <strong><code><span class="evidence">sudo apt-get update</span></code></strong>, <strong><code><span class="evidence">sudo apt-get upgrade</span></code></strong>, and <strong><code><span class="evidence">sudo apt-get dist-upgrade</span></code></strong>. Some people tend to add <strong><code><span class="evidence">&&</span></code></strong> and <strong><code><span class="evidence">-y</span></code></strong> but I don't really mind so I do them one at a time in case there are errors.

Lastly reboot the system and use nomodeset to login again. At this point you're an expert at adding nomodeset to the boot commands so just assume anytime there is a reboot (unless otherwise stated) just add nomodeset to boot.

<h2>2.a (Optional) Kernel Update</h2>
I like to run the latest RC kernel because there's generally better compatibility with new hardware but it's not neccesarily 100% stable. More like 98% stable in my experience. Given the new hardware I atleast recommend preforming a kernel update to the latest kernel (non RC) to be safe but it's optional.

Click [here](http://kernel.ubuntu.com/~kernel-ppa/mainline/) to see the latest kernel builds:
<ol>
<li>From the link above find the folder for the latest kernel (in my case at the time of writing this is 4.8-rc6 but 4.7 is the latest final release)</li>
<li> Depending on your distribution download 3 deb files for your distro. In my case I am running generic linux (default) and need the following deb files: <pre>linux-headers-4.8.0-040800rc6_4.8.0-040800rc6.201609121119_all.deb
linux-headers-4.8.0-040800rc6-generic_4.8.0-040800rc6.201609121119_amd64.deb
linux-image-4.8.0-040800rc6-generic_4.8.0-040800rc6.201609121119_amd64.deb</pre></li>
<li> Move the files to an empty folder, open terminal and cd to that folder</li>
<li> In order to install the kernels type: <strong><code><span class="evidence">sudo dpkg -i *.deb</span></code></strong> which will install each of the deb files you downloaded</li>
<li> After completing the install restart the computer and login</li>
</ol>

<h2> 3.Add the Graphics PPA </h2>
Open terminal and type <strong><code><span class="evidence">sudo add-apt-repository ppa:graphics-drivers/ppa</span></code></strong> then run <strong><code><span class="evidence">sudo apt-get update</span></code></strong>.

<h2> 4. Logout and Remove Nouveau</h2>
Some people say removing nouveau isn't neccesary, but in my experience it causes more problems when disabled and tends to restart itself during updates. As a result I recommend removing nouveau. In order to remove nouveau, disbale the desktop environment, and install the graphics drivers do the following:

<ol>
<li> Logout of your account and at the login screen type <kbd>CTRL</kbd>+<kbd>ALT</kbd>+<kbd>F1</kbd> to switch to "tty1"</li>
<li> Type your username and password into the console to login to your account</li>
<li> Depedning on your desktop environment, type either <strong><code><span class="evidence">sudo service gdm stop</span></code></strong> or <strong><code><span class="evidence">sudo service lightdm stop</span></code></strong> to disable the desktop envrionment</li>
<li>Next remove nouveau with by typing: <strong><code><span class="evidence">sudo apt-get --purge remove xserver-xorg-video-nouveau</span></code></strong></li>
<li> Now that nouveau is removed, we can go ahead and install the latest nvidia driver by typing <strong><code><span class="evidence">sudo apt-get intall nvidia-</span></code></strong> and pressing <kbd>TAB</kbd> to see the drivers available</li>
<li> In my case the latest driver (highest number after nvidia-) was "nvidia-370" so I installed the driver by typing <strong><code><span class="evidence">sudo apt-get intall nvidia-370</span></code></strong></li>
</ol>


<h2> 5. Reboot the OS and Test</h2>
The final step is to type <strong><code><span class="evidence">sudo reboot-</span></code></strong> to restart the computer. This time you <strong><em> do not</em></strong> need to type nomodeset at the grub menu. If all goes well you should be able to boot into the OS without any problems.

So far I have been able to successfully run the latest nvidia GPUs on the following systems multiple times with these steps:

Desktops:

| Motherboard | Proccessor | GPU |
|:-------|:-----------|:-------|
| Asus Maximus VIII Gene  | i7 6700k    | Titan XP  |
|Asus Z170 Pro Gaming|i7 6700   | GTX 1080 and 1070|
|Gigabyte Z170 Wifi|i5 6600k   | GTX 1070 |

Laptops:
Dell XPS 15 9550, Surface Book w. DGPU (both of these needed additional tweaks to install and run a dual boot but the graphics card install was identical)


 If the install fails I recommend the following trouble-shooting steps:

<ul>
<li>If you get the login screen but can't get the desktop, swithc to TTY and check the permissions of the .Xauthority file in your home folder</li>
<li>If you're getting a flickering screen and no login screen, switch to TTY and try to stop the display manager and repair the install there</li> 
</ul>