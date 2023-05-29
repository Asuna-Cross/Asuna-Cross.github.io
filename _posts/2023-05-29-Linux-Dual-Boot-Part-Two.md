---
title: Dual Booting Part 2, Installing Linux
date: 2023-05-29 
categories: [Operating Systems, Linux]
tags: [bootable devices, os install, linux]     # TAG names should always be lowercase
---

## Introduction

Now that we have the USB stick to boot from it is time to do the installation.

These instructions can be seen as a basis for all other types of laptops as general concepts are the same, however, they will be specific to the MSI Katana range that my laptop is from as this is what I have installed this onto and there were some issues that I can across that were specific to the hardware I have.

## Initial BIOS Changes

To start with this there are a couple of BIOS changes I had to make to my laptop to proceed.

To open up the BIOS I had to find out which button to press at startup, for this specific laptop that button is ``DEL`` , for others it may be different.

Once the BIOS has opened up it can be navigated using the arrow keys, the MSI BIOS also allows for navigation using the trackpad too.

The changes I did here was to turn the secure boot off and to change the order that the BIOS will boot from to put booting from USB higher than booting from the hard drive.

Once those changes were made it was time to save and exit with the USB disk plugged in to boot from.

### Explaining Turning Off Secure Boot
Turning the secure boot off was done as otherwise it would cause issues further down the line that are hard to solve, I wasn't able to solve them the last time I dual booted on my last machine without turning the secure boot off and this time around I wished to avoid that headache from the start.

For those of you unaware, secure boot helps to stop any unauthorised changes done to your computer at a BIOS level, by turning it off you are more susceptible to attacks such as keyloggers. However, after talking it out with a security professional I know it's better in my case to have it turned off for ease of access, as the attacks that the secure boot stops are highly specialised and take too many resources to undertake than would be spent on your regular person.

If there comes a time when I become a higher value target and the possibility of being attacked in ways secure boot will protect my machine then I will figure out how to make it work then.

## Installation
After you've exited the BIOS, if the USB is installed then it will automatically boot from it.

On Mint, you will be greeted with a desktop that will have a program to install Mint onto your machine.

The setup from there is pretty self-explanatory, the only things to keep in mind are that you need to click to keep both OS installed and to set up your partition correctly.

For my machine, I picked a near 50/50 split between my Windows and Linux machines for hard drive space. The reasoning behind this is that my Linux machine is for all thing security and development, while my Windows installation will be for music production and gaming (Both hobbies of mine). Overall, each side has the same amount of storage that my old machine had in total.

## Back Into BIOS
After the installation has been completed it is time to go back into the BIOS, remove the USB when prompted by your computer and reboot the machine.

Look for the ability to set the UEFI boot order. This will determine the order in which the OS are booted, when you find this move Linux to the top so that it boots first.

This was an issue that I was having with my machine, I had completed the installation and tried to reboot to see if I was successful and it kept booting to Windows.

After much searching I found that the boot order had to be changed to allow Linux to boot before Windows, this is because Linux gives you an option as to which OS you want to boot each time the laptop is turned on, while Windows assumes that if it's first in line that you want that and nothing else.

## SUCCESS!
Linux is now successfully installed and the dual boot is complete, all that is needed is to set up Linux, I used automation for mine which I will talk about in the next post.

### A Note About Graphics Cards
If your machine doesn't have a dedicated graphics card then you can skip this section, however, as mine does I will talk through what happened.

After the Linux installation had been confirmed as successful, which took several attempts to complete the installer, the OS wouldn't boot correctly, would hang or have graphical problems due to there not being the drivers to successfully interact with the graphics card correctly.

Getting this set up was part knowledge and part luck. On the load that it was stable enough I used the setup to set the drivers to the Nvida produced drivers which stabled the machine and made Linux operatable. However, this was pure luck to if the machine would stay alive long enough for this to happen.

If you know of any ways of making this less luck and more procedural then please contact me so I can keep it in mind for future installations.