---
layout: post
category: knowledge-base
title: HOWTO Install Windows 10 IoT Core on Raspberry PI 2 from a VM
date: 07 Jun 2015
tags: HOWTO RaspberryPI Windows10IoT VM VMWare
---

The boss of my new company I'm working for ordered two Raspberry PI 2 for experimental purposes. The reason for buying two of them was to have one Raspberry running a Linux distribution and the other one running Windows 10 IoT Core.


To install an operating system on a Raspberry PI the image of the operating system has to be put on a SD card. Putting the Linux distribution on a SD card was very easy. We only had to download the desired image from [RaspberryPI.org Downloads](https://www.raspberrypi.org/downloads/), insert the SD card into the card reader and then copy the image onto the card.

Putting the Windows 10 IoT Core version on the SD card was more difficult. According the [Get started with Windows 10 IoT Core and Raspberry PI 2](http://ms-iot.github.io/content/en-US/win10/SetupRPI.htm) you have to have a physical machine with *Windows 10 IoT Core Insider Preview* installed on it to put the Windows 10 IoT Core image to the SD card. The only problem by putting the image on the SD card with a VM is, that the VM has to have full access to the SD card reader. Because we didn't have an empty computer around to install *Windows 10 IoT Core Insider Preview* on it, I searched for a possibility to do it anyhow with a Virtual Machine. I asked [Google](https://www.google.ch) for help and Google answered me with [Ben Emmets post](https://www.simple-talk.com/blogs/2015/05/03/setting-up-windows-10-iot-core-on-raspberry-pi-from-a-vm/#.VXGrn8SpFsI.twitter) about *Setting up Windows 10 IoT Core on Raspberry Pi from a VM*. Following Ben Emmets instructions led to success. Thanks to Ben Emmet for this very helpful post!

**NOTE**: To make the SD card reader device visible in VM settings after unmounting the SD card reader from the host system I had to restart the VMWare Workstation. 


#### Links

* [RaspberryPI.org Downloads](https://www.raspberrypi.org/downloads/)
* [Get started with Windows 10 IoT Core and Raspberry PI 2](http://ms-iot.github.io/content/en-US/win10/SetupRPI.htm)
* [Ben Emmets post](https://www.simple-talk.com/blogs/2015/05/03/setting-up-windows-10-iot-core-on-raspberry-pi-from-a-vm/#.VXGrn8SpFsI.twitter)