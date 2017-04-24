---
layout: post
category: knowledge-base
title: Get NetworkCredential from PSCredential splits Username into Username and Domain
date: 13 Apr 2017
tags: .NET C# PowerShell
---

During development of a PowerShell binary module I had to do deal with two different credential types (`System.Management.Automation.PSCredential` and `System.Net.NetworkCredential`) and came across a behaviour I wanted to write down. 

The PowerShell binary module I developed contains several Cmdlets. One of them defines a parameter of type `System.Management.Automation.PSCredential`. Inside the Cmdlet we need to have an object of type `System.Net.NetworkCredential`. Getting such an object is easy as the `System.Management.Automation.PSCredential` provides an instance method called `GetNetworkCredential()`, which returns an object of type `System.Net.NetworkCredential`. This is the point I came across a behaviour I didn't expect. I expected `GetNetworkCredential()` method to return a new `NetworkCredential` object with exactly the same the `UserName` and `Password` as the corresponding `System.Management.Automation.PSCredential` object. However in case the `UserName` property of the `System.Management.Automation.PSCredential` object contains a domain part the `UserName` property of the `System.Net.NetworkCredential` returned by `GetNetworkCredential()` does not contain the domain part anymore. The domain part gets cut and assigned to the `Domain` property of the `System.Net.NetworkCredential` as shown in the following code sample.

```
PS C:\>$usernameWithDomain = 'my-domain\arbitraryUser';
PS C:\>$password = 'P@ssw0rd';

PS C:\>$psCredential = [System.Management.Automation.PSCredential]::new($username, (ConvertTo-SecureString -AsPlainText -String $password -Force));
PS C:\>$psCredential.UserName;
my-domain\arbitraryUser

PS C:\>$networkCredentialFromPSCredential = $psCredential.GetNetworkCredential();
PS C:\>$networkCredentialFromPSCredential.UserName;
arbitraryUser
PS C:\>$networkCredentialFromPSCredential.Domain;
my-domain
```

The reason behind this behaviour is, that `System.Net.NetworkCredential`, in contrast to `System.Management.Automation.PSCredential`, has a `Domain` property, which will be filled up with the domain part of the `UserName`.
