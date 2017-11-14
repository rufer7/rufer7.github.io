---
layout: post
category: knowledge-base
title: BUG "Task Scheduler service is not available" Error, if specifying Network Connection Condition
date: 14 Nov 2017
tags: bug Scheduled-Task Windows Feedback-Hub
---

There is a bug in Task Scheduler of Windows 10. If the network condition of a Scheduled Task gets enabled and a specific network connection gets selected, the corresponding Scheduled Task will not run anymore. To reproduce the problem open properties of any Scheduled Task (right click on Scheduled Task -&gt; `Properties`) and switch to the `Conditions` tab. Tick the box `Start only if the following network connection is available` and select a specific network condition.

<a href="{{ site.url }}/assets/screenshots/2017-11-13-scheduledtask-conditions.png"><img src="{{ site.url }}/assets/screenshots/2017-11-13-scheduledtask-conditions.png" alt="Scheduled Task - Conditions" /></a>

Click `Ok` and try to run the before edited Scheduled Task manually (right click on Scheduled Task -&gt; `Run`). When doing so the following error message pops up:

`Task Scheduler service is not available. Task Scheduler will attempt to reconnect to it.`

<a href="{{ site.url }}/assets/screenshots/2017-11-13-scheduledtask-error-message.png"><img src="{{ site.url }}/assets/screenshots/2017-11-13-scheduledtask-error-message.png" alt="Scheduled Task - Error Message" /></a>

If `Any connection` instead of a specific connection gets selected or if the network condition gets disabled at all, the Scheduled Task runs again perfectly fine.



A search on the Internet for this problem indicated, that a few other people had the same problem.

- [https://answers.microsoft.com/en-us/windows/forum/windows_10-update/task-scheduler-service-is-not-available/37d9625d-c600-422d-9aec-9a5707643b43](https://answers.microsoft.com/en-us/windows/forum/windows_10-update/task-scheduler-service-is-not-available/37d9625d-c600-422d-9aec-9a5707643b43)
- [https://answers.microsoft.com/en-us/windows/forum/windows_10-other_settings/task-scheduler-service-is-not-available-network/bc416b46-c247-4850-8ae6-9168ab997e20](https://answers.microsoft.com/en-us/windows/forum/windows_10-other_settings/task-scheduler-service-is-not-available-network/bc416b46-c247-4850-8ae6-9168ab997e20)


However I could not find any entries in Microsoft Knowledge Base or Microsoft Connect. Because of that I decided to report a problem via Microsoft Feedback Hub. My feedback can be found [here](https://aka.ms/S1fpd3). Please upvote!
