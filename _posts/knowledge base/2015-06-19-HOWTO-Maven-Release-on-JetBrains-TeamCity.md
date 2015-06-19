---
layout: post
category: knowledge-base
title: HOWTO Maven Release on JetBrains TeamCity
date: 19 Jun 2015
tags: CI/CD JetBrains TeamCity Java maven
---

In this post I'll show you how to set up a java build job for building and releasing a maven artifact. The [activiti wrapper](https://github.com/dfch/biz.dfch.j.activiti.wrapper) will be used as an example project. It's a maven project that will be released by using the [Maven Release plugin](http://maven.apache.org/maven-release/maven-release-plugin/).


Before creating build configuraitons for java projects, the following conditions must be met on the host system:

*HINT*: The TeamCity instance used here has no external build agents configured and runs under system account.

* [GIT](https://git-scm.com/downloads) installed
  * Git username and email for system set

    `git config --system user.name "John Doe"`

    `git config --system user.email john.doe@example.com`
* [Maven 3.2.5](https://maven.apache.org/download.cgi) installed ([Installation manual by Mkyong](http://www.mkyong.com/maven/how-to-install-maven-in-windows/))
* [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) installed


### Setup

Go to your TeamCity server and perform the follwing steps

* Create a new project from URL
    * Enter the repository URL, the username and the password as demanded
* Navigate to the settings of the newly crated project
* Under VCS Roots you can edit the existing VCS root to define the branch to check out (in our case this would be the `release` branch)

  <a href="{{ site.url }}/assets/screenshots/tc-mvn-release-vcs-1.png"><img src="https://dfch.files.wordpress.com/2015/06/tc-mvn-release-vcs-1.png?w=300" alt="TC-mvn-release-vcs-1" width="300" height="254" /></a>

  <a href="{{ site.url }}/assets/screenshots/tc-mvn-release-vcs-2.png"><img src="https://dfch.files.wordpress.com/2015/06/tc-mvn-release-vcs-2.png?w=300" alt="TC-mvn-release-vcs-2" width="300" height="261" /></a>

* Upload the maven settings.xml file which should be used for the release to the TeamCity server

  <a href="{{ site.url }}/assets/screenshots/tc-mvn-release-mvn-settings.png"><img src="{{ site.url }}/assets/screenshots/tc-mvn-release-mvn-settings.png?w=300" alt="TC-mvn-release-mvn-settings" width="300" height="62" /></a>

* Go to General Settings, choose the auto detected build configuration and click on `edit` (NOTE: In this sample there are two configurations because one of them was added manually in advance)

  <a href="{{ site.url }}/assets/screenshots/tc-mvn-release-general.png"><img src="https://dfch.files.wordpress.com/2015/06/tc-mvn-release-general.png?w=300" alt="TC-mvn-release-general" width="300" height="112" /></a>

* Navigate to the Version Control Settings and change the VCS checkout mode to `Automatically on Agent`

  <a href="{{ site.url }}/assets/screenshots/tc-mvn-release-vcs-chekcout-options.png"><img src="{{ site.url }}/assets/screenshots/tc-mvn-release-vcs-chekcout-options.png?w=300" alt="TC-mvn-release-vcs-chekcout-options" width="300" height="136" /></a>

* Go to the Build Steps menu, delete the existing build step and create two new build steps
  * Build step for release:prepare

    <a href="{{ site.url }}/assets/screenshots/tc-mvn-release-prepare-step.png"><img src="{{ site.url }}/assets/screenshots/tc-mvn-release-prepare-step.png?w=300" alt="TC-mvn-release-prepare-step" width="300" height="164" /></a>

  * Build step for release:perform

    <a href="{{ site.url }}/assets/screenshots/tc-mvn-release-perform-step.png"><img src="{{ site.url }}/assets/screenshots/tc-mvn-release-perform-step.png?w=300" alt="TC-mvn-release-perform-step" width="300" height="146" /></a>

* Last but not least the parameters referenced in the build configuration (release:prepare) have to be defined
  * Go to Parameters menu and define the following parameters to be prompted
    * env.development.version
    * env.git.password
    * env.git.username
    * env.release.version
  
  <a href="{{ site.url }}/assets/screenshots/tc-mvn-release-parameters.png"><img src="{{ site.url }}/assets/screenshots/tc-mvn-release-parameters.png?w=300" alt="TC-mvn-release-parameters" width="300" height="48" /></a>

  The parameters were specified as follows
  
  <a href="{{ site.url }}/assets/screenshots/tc-mvn-release-parameters-popup.png"><img src="{{ site.url }}/assets/screenshots/tc-mvn-release-parameters-popup.png?w=300" alt="TC-mvn-release-parameters-popup" width="300" height="209" /></a>


### Troubleshooting

#### Maven release:prepare hangs

Almost always the release:prepare goal of the maven release plugin hangs, the problem is that the GIT password is not set. In such a case the actual build has to be stopped and the password has to be set (i.e. according the manual above)


#### JRE instead of JDK

If the error message `No compiler is provided in this environment. Perhaps you are running on a JRE rather than a JDK?` occurs while the maven release plugin is preparing the release you have to install a java JDK on the build agents host system.

    [ERROR] COMPILATION ERROR :
    [INFO] -------------------------------------------------------------
    [ERROR] No compiler is provided in this environment. Perhaps you are running on a JRE rather than a JDK?
    [INFO] 1 error
    [INFO] -------------------------------------------------------------
    [INFO] ------------------------------------------------------------------------
    [INFO] BUILD FAILURE
    [INFO] ------------------------------------------------------------------------

#### Please tell me who you are

If the error message `Please tell me who you are` occurs on maven release:prepare the following commands have to be run on the build agents host system:

`git config --system user.name "John Doe"`

`git config --system user.email john.doe@example.com`