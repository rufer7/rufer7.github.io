---
layout: post
category: knowledge-base
title: HOWTO Analyze PowerShell Scripts with PSScriptAnalyzer
date: 16 Sep 2016
tags: PowerShell
---

A few weeks ago we started publishing our PowerShell modules to [PowerShell Gallery](https://www.powershellgallery.com/). After publishing the module [biz.dfch.PS.Appclusive.Client](https://github.com/dfensgmbh/biz.dfch.PS.Appclusive.Client) the first time we got an email from PowerShell gallery with some code analysis results with severity `Error`. As written in the email the analysis was performed with a module called [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer). We considered the project description and documentation at GitHub and were excited. The [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer) is a static code checker for Windows PowerShell modules and scripts. It checks the quality of scripts, Cmdlets, module manifest and module definition against a set of rules. The code checker Cmdlet returns code analysis results with different severities including suggestions for improvements.

Last week we played around with the PSScriptAnalyzer by checking the above mentioned PowerShell module ourselves with the `PSScriptAnalyzer`. The analysis of the diagnostic results revealed, that some of them were false positives. We identified them and then suppressed them. All the other results were very helpful to identify errors, unused variables, missing help in Cmdlets, etc.
The non suppressed results got corrected and now there are only a few `Warnings` left, which we could not suppress.

In the next sections I'll show you how to install the PSScriptAnalyzer and provide a summary with different usages of the `Invoke-ScriptAnalyzer` Cmdlet

#### Installation/Setup

The easiest way to install the `PSScriptAnalyzer` is, by using the `Install-Module` Cmdlet of `PowerShellGet` in combination with PowerShell 5.

`Install-Module -Name PSScriptAnalyzer`

#### Analyze

* Analyze a single PowerShell file

  ```
  Invoke-ScriptAnalyzer -Path PATH_TO_SCRIPT_FILE
  ```

* Analyze all PowerShell files in a specific folder and its sub folders

  ```
  Invoke-ScriptAnalyzer -Path PATH_TO_SCRIPT_FOLDER -Recurse
  ```

* Exclude some rules from the analysis

  ```
  Invoke-ScriptAnalyzer -Path PATH_TO_SCRIPT_FOLDER -Recurse -ExcludeRule "PSAvoidUsingCmdletAliases", "PSAvoidGlobalVars"
  ```

* Do analysis by applying only one specific rule

  ```
  Invoke-ScriptAnalyzer -Path PATH_TO_SCRIPT_FOLDER -Recurse -IncludeRule "PSAvoidGlobalVars"
  ```

#### Suppress

False positives can be suppressed by decorating scripts/functions with .NET's `SuppressMessageAttribute's`. For more details see [here](https://github.com/PowerShell/PSScriptAnalyzer#suppressing-rules)

#### Conclusion

After palying around with `PSScriptAnalyzer` I started doing the analysis as part of code reviews. As a next step I'll check how I could easily integrate the [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer) into our publishing process on TeamCity. I'll write another blog post about that as soon as I have integrated it.
