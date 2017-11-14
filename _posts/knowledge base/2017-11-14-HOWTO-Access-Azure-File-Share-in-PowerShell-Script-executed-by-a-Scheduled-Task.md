---
layout: post
category: knowledge-base
title: HOWTO Access Azure File Share in PowerShell Script executed by a Scheduled Task
date: 14 Nov 2017
tags: Azure PowerShell Scheduled-Task
---

Last week I had to set up an [Azure File Share](https://docs.microsoft.com/en-us/azure/storage/files/storage-files-introduction) for data transfer purposes. Clients will upload data to the Azure File Share and the data will then be moved from the share to a local drive by a PowerShell script. The PowerShell script gets invoked every 15 minutes by a Scheduled Task. 

The setup worked as expected but during the first tests a problem occurred. The script could not access the Azure File Share, that got mounted before with PowerShell. Opening a new PowerShell console and accessing Azure File Share worked fine; even if starting PowerShell as administrator. It seems that the Scheduled Task gets executed under a different security context even if the specified user account gets used when running the task. I solved the problem by mounting the Azure File Share (if not yet mounted) in the script using credentials from a configuration file.

In the next sections I'll explain how I set up the Azure File Share and the Scheduled Task and how the Azure File Share gets mounted in the data transfer script.

#### Azure File Share

To create an Azure File Share I just followed the official documentation.

1. [Create a storage account](https://docs.microsoft.com/en-us/azure/storage/common/storage-create-storage-account?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
2. [Create a file share in Azure Files](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-create-file-share)

After creation the Azure File Share can be mounted in Windows with File Explorer, Command Prompt or PowerShell (for details see [`Mount an Azure File share and access the share in Windows`](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows)). I mounted the Azure File Share under the actual user with PowerShell and could successfully access the share using File Explorer and PowerShell.

#### PowerShell Script for Data Transfer

First the connection credentials to mount the Azure File Share have to be exported to a configuration file.

1. Open PowerShell console as administrator
1. Create a credential object (Username and password according section `Mount the Azure File share with File Explorer` of [Mount on Windows](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows)) and export the credential to a configuration file

    ```PowerShell
    $cred = Get-Credential;
    $cred | Export-Clixml C:\PATH\TO\DataTransferConfig.xml;
    ```

In the data transfer script itself the credential can then be loaded using the following code snippet.

```PowerShell
$azureCredential = Import-CliXml $PathToConfigFile;
```

The `$PathToConfigFile` can either be specified in the script itself or can be passed to the script via a parameter.

Now the Azure File Share can be mounted in the script using the following code, where `$unc` contains the path to the Azure File Share (i.e `\\servername\azure-file-share-name`).

```PowerShell
if (!(Test-Path -Path $unc))
{
    New-PSDrive -Name "Y" -PSProvider "FileSystem" -Root $unc -Credential $azureCredential -Persist;
}
```

#### Scheduled Task

Last but not least the Scheduled Task, that executes the data transfer script, has to be created.

1. Open `Task Scheduler`
1. Create new task

    `Action` &gt; `Create Task...`

1. General Settings
    * Enter Name
    * Select `Run wheter user is logged in or not`
    * Tick `Run with highest privileges`
    
    <a href="{{ site.url }}/assets/screenshots/2017-11-07_01_scheduledtask_azurefileshare_server_general.png"><img src="{{ site.url }}/assets/screenshots/2017-11-07_01_scheduledtask_azurefileshare_server_general.png" alt="Scheduled Task Azure File Share - General" /></a>
    
1. Create new trigger

    <a href="{{ site.url }}/assets/screenshots/2017-11-07_02_scheduledtask_azurefileshare_trigger.png"><img src="{{ site.url }}/assets/screenshots/2017-11-07_02_scheduledtask_azurefileshare_trigger.png" alt="Scheduled Task Azure File Share - Trigger" /></a>

1. Create new action

    <a href="{{ site.url }}/assets/screenshots/2017-07-12_05_scheduledtask_azurefileshare_action.png"><img src="{{ site.url }}/assets/screenshots/2017-07-12_05_scheduledtask_azurefileshare_action.png" alt="Scheduled Task Azure File Share - Action" /></a>

    **Add arguments:** `-ExecutionPolicy RemoteSigned C:\PATH\TO\Move-Data.ps1 -PathToConfigFile C:\PATH\TO\DataTransferConfig.xml`
