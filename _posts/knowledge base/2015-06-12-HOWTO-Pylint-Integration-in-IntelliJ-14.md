---
layout: post
category: knowledge-base
title: HOWTO Pylint Integration in IntelliJ 14
date: 12 Jun 2015
tags: IntelliJ IDEA JetBrains python Pylint
---

I was asked, if it's possible to integrate [pylint](http://www.pylint.org/) into JetBrains IntelliJ IDEA 14. After having a quick look at Google I found a [blog post](http://sysmagazine.com/posts/163227/) about the integration of pylint. The mentioned blog post references an older IntelliJ version and the author runs IntelliJ on Linux. Because I run IntelliJ 14 on Windows I decided to shortly describe the configuration for this combination here.


I presuppose that IntelliJ 14, [python](https://www.python.org/) and pylint are installed and that the following path are added to the Windows `PATH` variable (Paths depend on the installation location)

* C:\python27
* C:\python27\Scripts

To integrate pylint into IntelliJ IDEA 14 open your IDEA and go to Settings (`Ctrl` + `Alt` + `s`)

* Navigate to `Tools` &gt; `External Tools`
<img src="{{ site.url }}/assets/screenshots/pylint-integration-IntelliJ-1.png" alt="pylint integration screnshot 1"/>


* Add a new External Tool by clicking on `+`
<img src="{{ site.url }}/assets/screenshots/pylint-integration-IntelliJ-2.png" alt="pylint integration screnshot 2"/>
In tool settings section you have to add the path to your `pylint.exe` file to the programm textfield. Referencing pylint.bat won't work.

* Add a new Output Filter
<img src="{{ site.url }}/assets/screenshots/pylint-integration-IntelliJ-3.png" alt="pylint integration screnshot 3"/>


Now as you are done you can execute pylint over the `Tools` menu
<img src="{{ site.url }}/assets/screenshots/pylint-integration-IntelliJ-5.png" alt="pylint integration screnshot 4"/>

The result of the pylint code analysis will then be printed to the run console in IntelliJ.

For more details and for Linux based configuration see [here](ref http://sysmagazine.com/posts/163227/)