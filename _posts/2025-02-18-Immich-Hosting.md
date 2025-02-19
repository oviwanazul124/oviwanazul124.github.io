---
title: ¿Immich a really good alternative?. I really think so...
date: 2025-02-18 12:16:53 +0100
categories: [Tech]
tags: [Tech, Opinion]
description: My opinion on using immich to autohost our own photos.
image:
  path: assets/photos/Immich-Opinion/Header.png
  alt: Immich Header
---


## What is immich?

Immich is an **open-source alternative** to any hosting cloud apps that save your photos. It has been a while since I heard about this, and because I had a **Raspberry Pi 4** and a boring 
night, and started to think about hosting in it. Is not the only alternative that is open-source or hostable, there are also many more like **Plex Photo** and **Next Cloud Photos**. But I heard so many good things about it that I need to try it on.

I am changing from **Google Photos** for two main reasons, the first of all is the problem I am having with **GMail**, recently I bought a new phone and transferred all of my old photos that mobile, the thing I didn't know is that Google Photos, automatically **started to do backups** without even knowing (Maybe it was my fault, I don't know), but then I started to see a pop-up saying that **I'm going to not receive any more emails** because I have too much GBs on Google Photos.

The other reason is more **focused on privacy**, I like privacy and surely in more future blogs, you will see that. I do not like the idea of a **big tech company getting all my private photos**, for any reason and using them **to study any stats or AI**. Also, there have been SOOOOO many **data leaks in big tech companies** that one day I'm going to be affected (I'm affected right now, and I am sick of all the "Notify" about my non-existent packages). 

## The setup

Now centering on the main setup of the **"server"** is a Raspberry Pi 4 with 4GB RAM, if you think about using this setup **I would recommend you use 8GB RAM** because sometimes this setup would crash my Raspberry.

![RaspberryPi4-Photo](assets/photos/Immich-Opinion/RaspberryPi4.webp)
_Raspberry Pi 4 model that I used_

The second most important thing in this setup would be the hard drive, in my case, **I'm using the SD card** of the Raspberry, yeah I can't afford right now one Hard Drive, but the only difference that would make it is **the speed of the upload of the photos**.


## Setting Up Immich

When I was setting up Immich **I followed the Immich [started guide](https://immich.app/docs/install/docker-compose)**, it was really simple I didn't encounter any problem, **only installing Docker in my machine**, I didn't know why but the tutorial on his main page didn't work on my machine so I found another tutorial from other page and it worked (If I found the tutorial I would link it here).

![Immich-Starte-Guide](assets/photos/Immich-Opinion/Photo-Tutorial-Page.png)
_Photo of the tuorial page_

The second thing I needed to do was enable the networking of the server, because in my case I had installed **Jail2Ban** in the machine and didn't remember about it, and it was a horror how I was trying to connect via SSH or any other connection and Jail2Ban disabled it, so check it out if your server has any of that.

Now it was connected, yeah it didn't take too much I think about **1 hour** (It includes the update from Raspberry that I didn't update for around two or three years, hahaha). The next thing that I needed to do was connect to the server, it was easy, and create the administrator account.

Then tested if it worked and yeah, now I can connect from my PC, but I don't take my PC when I am out taking photos with my friends or the scenery, I need to set it up on my phone. Here it was a really easy process I mean it was only installing it from the Play Store and setting up my account, but I encountered a problem maybe it was dark at that moment because I was around 15 minutes trying to upload a photo, if you do not know how to upload right now I didn't find an option to upload a specific photo and only found how to backup and album.

## My Final Opinion

Well finishing with this I liked the project it was easier to use and set up and I am looking forward to all the things that are shown in the roadmap like the photo editor or the private photo. I would like in the future to contribute to the [project](https://github.com/immich-app/immich) (If you know the languages used, be sure to contribute to making it even better)
