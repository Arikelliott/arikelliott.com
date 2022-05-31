---
title: "Adventures in Virtualization - Part 1"
date: 2022-05-30T11:30:03-04:00
draft: true
---

As a Linux user, I have a problem that many Linux users face: what do you do if you want to run a program that will absolutely, definitely only run in Windows? You've tried finding a Linux version, finding a good alternative, and getting it to run in Wine/Proton/Lutris/etc. and nothing has worked. You need that program, and it needs Windows.

You could dual boot, but switching over to Windows for one program breaks your workflow. You have to stop and close every other thing you're doing, then spend a while restarting your computer and booting Windows up. If there's anything I've seen push people back to Windows despite their best attempts to switch to Linux, it's this.

Fortunately, we have a solution: virtual machines. What if you could run Windows and Linux at the same time, on the same PC, and easily use both at once? We can!

## Virtual Machines

Virtual machines probably aren't new news to anyone reading this. A lot of Linux users, at least the more recent ones, probably got started trying out Linux in a virtual machine before installing it on their PC. My very first experience with Linux I went straight for a dual boot setup with Windows 7 and Linux Mint (which didn't last before I went back to only Windows), but every time since then I've used Oracle's VirtualBox to try things and it was only quite a bit of messing around that I made the jump.

Unfortunately, every VM vendor, whether it's VirtualBox, VMware, QEMU/KVM, or others, has a common issue: graphics.

You see, with most parts of our PC's hardware, whether it's your CPU, RAM, or hard drive, we can easily split up the resources we have available to us to give some to the VM and keep some for the native OS running it. But not our GPUs. Those are all or nothing: you either give your VM the whole GPU, or none of it.

*Note:* There's technically some exceptions to this. Some server/workstation GPUs, such as Nvidia's Tesla GPUs, *are* able to be split up. Also, from my understanding, everything we need to split up computer GPU resources exists and is ready to use, we're just waiting on companies to make GPUs that support it. [(Here's a good Level1 Techs video on that for those interested)](https://www.youtube.com/watch?v=IXUS1W7Ifys)

So what does that mean? Virtual machines **do** still have, y'know, graphics... right? 

Sort of.

## The GPU Problem

Admittedly I'm not an expert on exactly how virtual machines handle graphics (or work in general. Keep that in mind: you don't have to be an expert to do this stuff!), but my rough understanding is that the CPU handles the graphics, something you wouldn't normally do with a CPU.

(For reference, normally your PC makes all the graphics/user interface stuff you see every day with GPU, either a graphics card plugged into your motherboard or a very small one built into your CPU)

This is an issue because it gives you only very basic graphics. Things that are graphically demanding can get sluggish, and some things you can count on not running at all. Speaking for myself, there's four uses I have for a Windows virtual machine: Microsoft Office, Adobe's Creative Cloud suite (Photoshop, Illustrator, etc.), games that don't run on Linux, and some 3D modeling. Out of those, MS Office is the only one that isn't slow or outright unusable in a regular VM.

Fortunately, there *is* a solution: **GPU Passthrough.**

# My Adventure Plan
---
I've got a particular use case for this. I'm going to explain what it is, how I've been figuring out how to do it, and why, and that should hopefully give you a starting point to apply it for your own uses.

## My setup: HOW many VMs??

For me, my main use for my PC is a Linux desktop. So whatever setup I put together, I need to be able to keep Linux running. Plus, I need a Windows VM I can spin up to do all that Windows-only stuff I mentioned on. After that, I'd like to be able to make more VMs as well, for uses such as running my own home webservers, game servers, utilities such as a NAS, PLEX servers, PiHole adblocker, and any other useful or educational things I may want to try.

Hardware-wise, my PC uses a Ryzen 9 5950X, AsRock X570 Steel Legend motherboard, four 8GB of RAM from Crucial, an RX 6700 XT, an Nvidia Quadro M2000, and a 







# Steps I've Taken So Far
---
## BIOS Settings

