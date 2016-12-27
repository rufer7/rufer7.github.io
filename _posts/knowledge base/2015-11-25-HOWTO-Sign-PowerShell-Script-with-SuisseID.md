---
layout: post
category: knowledge-base
title: HOWTO Sign PowerShell Script with SuisseID
date: 25 Nov 2015
tags: PowerShell SuisseID
---

At d-fens, the company I'm working for, we all have a [SuisseID](www.post.ch/suisseid‎), which can be used for different purposes like authentication and electronical signing purposes. It's as well possible to sign code with the SuisseID. The advantages of using the SuisseID for code signing are that the SuisseID is a very cheap in comparison to other code signing certificates and that the user gets authenticated personally. The following section describes the necessary step to sign a PowerShell script on Windows by using your SuisseID.

To sign code with your SuisseId using PowerShell your SuisseId has to be installed on your computer and as well has to be connected with your computer.

1. Open the Microsoft Management Console (`mmc.exe`)
1. Press `Ctrl + m`
1. Add `Certificates` to the `Selected snap-ins`
1. On pop up select `My User Account`
1. Open the certificates tree and navigate to `Personal\Certificates`
1. Select the SuisseId `Qualified Signature` certificate (Issued by `SwissSign Qualified Platinum CA 2010 - G2`)
1. Right click -> Properties
1. In `General` tab select the radio button `Enable only the following purposes`
1. Apply
1. Open a new PowerShell session (Run as administrator)
1. Get your code signing certificate by esecuting the following command
  
  ```$cert = Get-ChildItem cert:\CurrentUser\my -CodeSigningCert```

1. Sign PowerShell script file by executing the following command

  ```Set-AuthenticodeSignature -FilePath C:\PathToTheFile\SomeFile.ps1 -Certificate $cert```
