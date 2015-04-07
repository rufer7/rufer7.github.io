---
layout: post
category: knowledge-base
title: IntelliJ - Setup custom inspection profiles
date: 07 Apr 2015
tags: inspection-profiles IntelliJ IDEA JetBrains
---

In most java projects I worked, compiling the source code in an IDE produced lots of warnings. Figure out which warnings could be ignored is very troublesome. In this blog post I will show you how to set up project specific inspection profiles in IntelliJ to avoid the output of ignorable warnings.


#### What's an inspection profile?

An inspection profile defines which inspection rules are enabled/disabled and the rules severity level. In other words inspection profiles define which types of problems should be logged through code inspection.


#### Create a new inspection profile

Creation of a new inspection profile is described under [Customizing Profiles @IDEA documentation](https://www.jetbrains.com/idea/help/customizing-profiles.html#d1529343e18596). As mentioned in the documentation the new profile is created as a copy of the default profile.

To set the newly created profile as a project specific inspection profile check `share to team members` as shown below

<img src="{{ site.url }}/assets/screenshots/share-inspection-profile.png" alt="IntelliJ IDEA screenshot"/>


In this case the profile is saved in XML-format under PROJECT_ROOT/.idea/inspectionProfiles.


#### Customize inspections profiles

Now the newly created profile can be adjusted according your wishes.

IntelliJ allows you to suppress certain inspections for a specific peace of code or for a whole file. Suppressing inspections can be done either from the editor or from the inspection tool window. More details about suppressing inspections in detail can be found under [Suppressing inspections @IDEA documentation](https://www.jetbrains.com/idea/help/suppressing-inspections.html).
I recommend to suppress all warnings, which could be ignored by developers, so that only warnings that have to be fixed will be printed out after inspection.