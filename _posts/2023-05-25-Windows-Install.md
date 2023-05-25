---
title: Windows 11 Installation
date: 2023-05-25 
categories: [Operating Systems, Windows]
tags: [windows, os install]     # TAG names should always be lowercase
---

## Background

Recently I upgraded to a new laptop as my old one was no longer able to keep up with the requests I was placing on it.

The new laptop has been dual booted with Linux and Windows, the next few posts will be details of how I set up both sides of my installation and how to dual boot based off of my experiences with the laptop.

For reference, the laptop is from the MSI Katana range, this will be important to know when it comes to the dual booting segment in a future post.

## Windows Installation

The machine came with Windows 11 built in already, during the set up it demanded access to the wifi so that my user account would be linked to an email address. This can be worked around to have a local account rather than an email linked one.

To do so I did the following.

``ctrl + F10``
This is to bring up the command prompt while in the starting setup

If you're at the screen where it is asking you to connect to an internet connection, then type in the following
``OOBE\BYPASSNRO``
This will restart your machine and set you back to the beginning of the installation process.

After you're back at the start, open up command prompt again and type in the following
``ipconfig /release``
This disconnects your internet temporarily.

After doing this, when you get to the part where it requests to go online you will get the option to continue offline and thus skip adding an email address to your OS setup.

Once that problem was out of the way the rest of the installation went smmothly. I was taken aback by the amount of additional tracking, and even adverts that Windows was informing me about for opting in or out of.

The first thing to do after the installation was to install all the patches to Windows and my drivers, thankfully Windows has an in-built system for this, unfortunately they have removed command line support for this in Windows 11, so if you are doing this yourself then you will need to find it in the GUI.

### Useful Tools

I would like to take the time to highlight some tools that I found incredibly useful when setting up my Windows machine.

The first is a piece of software called [BloatyNosy](https://www.builtbybel.com/blog/about-bloatynosy), this software removes bloatware and toggles all others that is in unable to uninstall to disable them.

When running it myself it was able to grab pretty much everything and removed a lot of things that were bothering me when Windows booted up.

The second piece of software that I used for all my installations is [Chocolately](https://community.chocolatey.org/) , this acts similar to ``apt install`` that Linux machines have, through this I was able to cut down the time needed to find all the software I wanted to install.

While I didn't take this route myself, you can pair up Chocolately with a piece of software called [Boxstarter](https://boxstarter.org/) for a fully automated Windows set up if repeatability is what you want.

Here is a tutorial from Windows Dev team as to how to use Boxstarter - https://devblogs.microsoft.com/cesardelatorre/automating-windows-environments-setup-with-boxstarter-and-chocolatey-packages/

I didn't go this route myself as my Windows machine won't be replicated that often, however if I do go the route of setting up Windows boxes and such for testing then it is an option that I will start to look at.
