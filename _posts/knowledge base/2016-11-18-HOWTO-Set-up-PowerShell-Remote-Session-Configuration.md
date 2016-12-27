---
layout: post
category: knowledge-base
title: HOWTO Set up PowerShell Remote Session Configuration
date: 18 Nov 2016
tags: PowerShell WinRM
---

Todays blog post is about setting up a PowerShell remote session configuration on a Windows machine. A PowerShell remote session configuration can be used when connecting from another machine (hereinafter called as `Client`) to the machine the PoSH remote session configuration resides on (hereinafter called as `Target`) using `Enter-PSSession` Cmdlet. A PoSH remote session configuration allows you to define under which user (Credential) the remote commands sent by the `Client` over the remote session will be executed. The `Client` only has to know the hostname of the `Target` and the name of the PowerShell session configuration.

#### Prerequisites

The following conditions have to be fullfilled to make it work.

* The user, who will enter the remote session from the `Client`, has to have remote login access on the `Target`
* To execute the `Enter-PSSession` Cmdlet without specifying the Credential, the `Client` and the `Target` have to be in the same domain or workgroup
* Both (`Client` and `Target`) must have valid SSL certificates

#### Target

To set up the PowerShell remote session configuration on the `Target` the following commands have to be executed.

```Powershell
Enable-PSRemoting -Force;

#### Configure WinRM to use HTTPS
winrm quickconfig -transport:https;
netsh firewall add portopening TCP 5986 "WinRM over HTTPS";

#### Register PowerShell session configuration
Register-PSSessionConfiguration -Name PSSESSION_CONFIG_NAME -RunAsCredential CREDENTIAL_TO_RUN_CMDS_WITH -ShowSecurityDescriptorUI;

#### Assign X.509 certificate to WinRM listener
$Thumbprint = (Get-ChildItem -Path Cert:\LocalMachine\My | Where-Object {$_.Subject -match "CERT_NAME"}).Thumbprint;
winrm set winrm/config/Listener?Address=*+Transport=HTTPS '@{Hostname="FULL_QUALIFIED_DOMAIN_NAME";CertificateThumbprint="THUMBPRINT_HERE"}';
```

#### Client

To enable windows remote management on the `Client` the following commands have to be executed **once** on the `Client`.

```Powershell
Enable-PSRemoting -Force;
winrm quickconfig -transport:https;
netsh firewall add portopening TCP 5986 "WinRM over HTTPS";
```

To test the connection from `Client` to `Target` execute the following command

```Powershell
Test-WsMan FULL_QUALIFIED_DOMAIN_NAME;
```

Now you can connect to the `Target` by entering the before defined PowerShell session configuration as follows.

```Powershell
Enter-PSSession -ComputerName FULL_QUALIFIED_DOMAIN_NAME_OF_TARGET -ConfigurationName PSSESSION_CONFIG_NAME -UseSSL;
```
