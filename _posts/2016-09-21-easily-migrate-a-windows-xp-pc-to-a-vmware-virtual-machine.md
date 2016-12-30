---
layout: post
title: Easily Migrate a Windows XP PC to a VMWare Virtual Machine
date: '2016-09-21 17:25'
author: bradleygmayne
comments: true
categories:
  - How-To
  - migrate
  - virtual machine
  - vm
  - vmware
  - xp
---

Recently the company I work for had a Windows XP machine that is the brain of a primary manufacturing process die on them. After switching out the power supply and taking into consideration that the machine was ancient I decided to buy a new box and convert the original to a virtual machine. What made it so difficult was that I didn't have the cpu box itself to backup and covert. I only had the hard out of the machine. So the plan was to put the hard drive into an external enclosure and use the new machine to do the conversion.

I found an application called [Symantec System Recovery - Server Edition](http://www.symantec.com/system-recovery-server-edition/trialware) that easily converted a system backup to a virtual machine very easily. The link takes you to the Veritas website but I assure you it is the same application. The link can be found at the bottom of the page.

- Download the trial version of the application which allows a 60 ay free trial and install it on the host machine.
- Create a backup of the drive from the old machine and save it on the host computer's drive.
- Now convert that backup to a virtual machine by selecting the fresh backup on the host and make sure to check the **Run Windows Mini-Setup** option. This was the kicker that made the whole conversion so simple. By adding this Windows mini-setup it allowed the VM to evaluate the VM machine setup and install new device drivers for the VM so that it will start up and run without any driver errors. _No system disk is necessary, it just works!_
- I used VMWare Workstation for my virtualization environment but you could use [VirtualBox](https://www.virtualbox.org/wiki/Downloads) which is free software from Oracle that works great as well. This is a great tutorial on how to use a VMWare .vmdk file with VirtualBox: [Techathlon.com - How to open a vmdk file in Oracle VirtualBox.](http://techathlon.com/how-to-run-a-vmdk-file-in-oracle-virtualbox/)
- Re-activating Windows is probably the most difficult thing you'll have to deal with. If you are converting Windows7 or newer you'll have no problem activating but XP is another story.

Windows XP is not supported by Microsoft anymore so when you try and activate it will just time out over and over. People all over the net suggest using the telephone activation feature which is supposed to work but I had no luck after attempting many times. _I presume you have a valid license for XP as I do not condone piracy._ The method that worked best for me can be found here: [My *nix world - Bypass Windows XP product activation](https://mynixworld.info/2012/12/19/bypass-windows-xp-license-activation/).

You should now be good to go but my migration involved a USB security dongle that presented a new set of challenges. That's going to be another post. Make sure an take a snapshot of the VM the second you get everything back up and running 100%. A perfect snapshot will allow you to easily jump right back to "perfect brand new machine" mode in about 2 min, roughly. Not a bad deal. Get an auto snapshot setup running and implement a robust backup regiment for your vm host machine.
