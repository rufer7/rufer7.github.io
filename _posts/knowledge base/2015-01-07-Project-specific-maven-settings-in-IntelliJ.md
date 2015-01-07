---
layout: post
category: knowledge-base
title: Project specific maven settings in IntelliJ
date: 07 Jan 2015
tags: IntelliJ IDEA JetBrains maven development
---

The company I'm working for has its specific maven settings file (settings.xml), which defines the repository, some profiles and so on. For a project on customer side I wanted to have another settings file in place without changing or extending the existing one.


By default IntelliJ 14 takes the user settings file under C:\Users\{user}\.m2\settings.xml. This can be manually overridden per project:

1. Go to settings (`Strg + Alt + s`)
2. Navigate to `Build, Execution, Deployment` > `Build tools` -> `Maven` (or search for `Maven`)
3. Select the `override` checkbox on the line of `user settings file` and refer the project specific settings.xml-file

<a href="{{ site.url }}/assets/screenshots/override-settings.xml.png" target="_blank">
    <img src="{{ site.url }}/assets/screenshots/override-settings.xml_thumbnail.png" alt="IDEA screenshot" border="1">
</a>