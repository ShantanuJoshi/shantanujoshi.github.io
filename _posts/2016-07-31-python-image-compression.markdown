---
title: "Compresssing Images in Python"
layout: post
date: 2016-07-31 15:08
tag: cs
image: 
headerImage: true
projects: false
blog: true
hidden: false # don't count this post in blog pagination
description: "Compressing Images for this Blog"
jemoji: 
author: shantanujoshi
externalLink: false
---
While working on website performance tuning for some part time work I needed to find a way to compress 100,000+ images for an ecommerce website's catalog. The current solution to image compression was a "designer" who would bulk process images in photoshop with a macro. He had worked for 4 days straight and estimated a 2 week completion time for processing all the pictures. 

The images were simply too large in file size and the wrong dimensions. Each image had to be both scaled to fit within fixed square pixel dimensions and reduced in file size. 

I wrote a pythons script (attached below) to compress the files for this specific task. But I thought I'd rewrite it to work for compressing images for this blog given that having a post with 15 10mb images would not be great for load times. 

Here's my version of the image compression script built for compressing images in a given directory to a managebale size using Pil (or Pillow) a python library that does most of the work here.

<strong> If you're looking for something that can also change image dimensions see [here](https://gist.github.com/ShantanuJoshi/44e9b72a985d5d6b4e8df2810ce5d25e) </strong>


<h2 id="heading2">CompressMe.py</h2>
<script src="https://gist.github.com/ShantanuJoshi/23ac55479ab9a613230bd9467d080f33.js"></script>