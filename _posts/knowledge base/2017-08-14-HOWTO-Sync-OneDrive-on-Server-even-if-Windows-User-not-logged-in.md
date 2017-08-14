---
layout: post
category: knowledge-base
title: HOWTO Sync OneDrive on Server even if Windows User not logged in
date: 11 Aug 2017
tags: Microsoft OneDrive Scheduled-Task Synchronisation
---

In a project for one of our customers we used [Microsoft OneDrive](https://onedrive.live.com) for data synchronisation. The data gets collected on a tablet and the folder containing the data will be synchronized with OneDrive. On the other side there is a Windows Server that needs to move the data from OneDrive to a network drive.

To get the data from OneDrive I installed the OneDrive Client Version 2016 (Build `17.3.6943.0625`) on the Server. Furthermore I created a scheduled task that executes a PowerShell script to copy the files from the synchronized OneDrive folder to the network drive. Unfortunately OneDrive only runs synchronization if the user, the OneDrive client was installed with, is logged in to Windows. As the user does not log in to the server regularly and because there is no possibilty to reconfigure OneDrive to allow synchronization even if the user is not logged in, I had to find a way to regularly synchronize the OneDrive folder. After a few tries I succeeded by creating a scheduled task that starts and stops OneDrive.exe on a given schedule.

The scheduled task was created as follows.

1. Open `Task Scheduler`
1. `Action` > `Create Task ...`
1. General configuration
    <a href="{{ site.url }}/assets/screenshots/2017-08-07_01_scheduledtask_onedrivesync_general.png"><img src="{{ site.url }}/assets/screenshots/2017-08-07_01_scheduledtask_onedrivesync_general.png" alt="Scheduled Task OneDrive Sync - General" /></a>
1. Create trigger
    <a href="{{ site.url }}/assets/screenshots/2017-08-07_01_scheduledtask_onedrivesync_trigger.png"><img src="{{ site.url }}/assets/screenshots/2017-08-07_01_scheduledtask_onedrivesync_trigger.png" alt="Scheduled Task OneDrive Sync - Trigger" /></a>
1. Create new action
    <a href="{{ site.url }}/assets/screenshots/2017-08-07_01_scheduledtask_onedrivesync_action.png"><img src="{{ site.url }}/assets/screenshots/2017-08-07_01_scheduledtask_onedrivesync_action.png" alt="Scheduled Task OneDrive Sync - Action" /></a>

    **Program/script:** `C:\Users\USERNAME\AppData\Local\Microsoft\OneDrive\OneDrive.exe`
1. Configure settings
    <a href="{{ site.url }}/assets/screenshots/2017-08-07_01_scheduledtask_onedrivesync_settings.png"><img src="{{ site.url }}/assets/screenshots/2017-08-07_01_scheduledtask_onedrivesync_settings.png" alt="Scheduled Task OneDrive Sync - Settings" /></a>
