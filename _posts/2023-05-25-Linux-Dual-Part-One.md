---
title: Dual Booting Part 1, Making the Bootable Device
date: 2023-05-25 
categories: [Operating Systems, Linux]
tags: [bootable devices, os install, linux]     # TAG names should always be lowercase
---

The second part in the series about dual booting my laptop.

This will cover how to creat the bootable device with a Linux distribution.

## Choosing Linux Distribution
The first thing to do was to pick a distribution of Linux that I was going to be using as my daily driver (Main OS for working)

To do this I set myself with several requirements that I wanted to have in an OS, these were the following :

- Had to be lightweight
- Have a Graphical User Interface (GUI)
- Capable of handling virtual machines (VM)
- Have long term support for security updates and patches


After I had set these requirements I asked around those who knew more than me to get their opinions and suggestions as to what they use for their own daily drivers. The overall consensus was that [Mint](https://linuxmint.com/) would be the best option for me.

The OS is stable and has a lot of features that I needed without having too many that it becomes bloated.

Mint itself has three versions, Cinnamon, MATE and Xfce. The Xfce is the lightest of the three distributions, which means that it doesn't use as much of your computers resources as other distributions would.

It is also currently in the long-term support schedule, which means that it will have support and security updates for the next few years, compared to others which will only have support for 6-months.

## Downloading the ISO

After choosing Mint, the next thing to do was to download the ISO file needed for it.

If you have experience using torrents and downloading large files you can skip this section.

If possible, the easiest way to download the ISO from one of the mirrors. Mirrors are people who are hosting the file on behalf of the owner so that there are options that are closer to the ones downloading it. If you chose this option then pick the option closest to yourself.

For those with unstable internet then the torrent version would be better.

To torrent the download you will need to have software installed that allows you to use the links. My personal recommendation and what I used for this was [Deluge](https://deluge-torrent.org/). I used this one as it is small and doesn't come with any of the additional features such as adverts that the bigger, more known options give you.

Once it's downloaded and installed it's quite easy to open it and add your link from the website into the downloader.

If you go the torrent route, please have some sort of way of checking the incoming traffic for viruses and trojan as some may attempt to come through. My choice for this was [MalwareBytes](https://www.malwarebytes.com/), if you wish to have a paid version then see if your bank or other providers will offer you a free key as part of their "keeping customers safe" schemes.

## Flashing USB Drive

After you have downloaded the ISO and verified it using the tutorial on the official website it comes time to put it on a USB drive to turn it into a drive that you can boot the OS from.

To do this you will need a spare USB that can hold the file. Hilariously enough, the device I used was a snap bracelet given out by the local college that had a USB drive on the end of it.

The simplest way of doing this is to download a piece of software called [etcher](https://etcher.balena.io/) that is made by balena.

Once downloaded it is very straight forward to use and gives step-by-step instructions as to what you need to do.

Just note, once this is done you will need to reformat your USB drive if you wish to use it for other purposes.
