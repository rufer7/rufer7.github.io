---
layout: post
category: knowledge-base
title: HOWTO Access Microsoft Access Database with PowerShell
date: 19 May 2017
tags: ODBC PowerShell
---

In one of our current projects we had to access a Microsoft Access Database (`.mdb`) with PowerShell. I first tried to access the `.mdb` using the `Invoke-SqlCmd` Cmdlet from our PowerShell module [`biz.dfch.PS.System.Data`](https://github.com/dfch/biz.dfch.PS.System.Data). Unfortunately connecting to the Access database with the `Invoke-SqlCmd` Cmdlet does not work as it uses `SqlClient` from the C#/.NET namespace `System.Data` under the hood. 

After a short internet research I figured out, that I have to use `System.Data.Odbc` or `System.Data.OleDb` from the C#/.NET namespace `System.Data`. I decided to use `System.Data.Odbc` and extended our current PowerShell module [`biz.dfch.PS.System.Data`](https://github.com/dfch/biz.dfch.PS.System.Data) accordingly. From version `2.0.0` the module [`biz.dfch.PS.System.Data`](https://github.com/dfch/biz.dfch.PS.System.Data) has a new Cmdlet called `Invoke-OdbcCmd`. The `Invoke-OdbcCmd` Cmdlet can be used to invoke commands against different databases that support `ODBC`.

#### Install Microsoft Access 2016 Runtime

To make `Invoke-OdbcCmd` Cmdlet work, the necessary driver has to be installed.

1. Download [Microsoft Access 2016 Runtime](https://www.microsoft.com/en-us/download/details.aspx?id=50040)
1. Install Microsoft Access 2016 Runtime

#### Install PowerShell Module biz.dfch.PS.System.Data

To install the PowerShell module [`biz.dfch.PS.System.Data`](https://github.com/dfch/biz.dfch.PS.System.Data) the following steps have to be executed.

1. Open PowerShell console
1. Download NuGet package by executing the following command

    `nuget install biz.dfch.PS.System.Data`

1. Install NuGet package by executing the following command

    `.\biz.dfch.PS.System.Data.2.0.0\Install.ps1`

#### Usage of Invoke-OdbcCmd Cmdlet

**Get identity from access database (.mdb or .accdb)**

```PowerShell
Invoke-OdbcCmd -Dbq 'C:\arbitrary-database.mdb' -Driver '{Microsoft Access Driver (*.mdb, *.accdb)}' "Select @@Identity";
```

**Login with credentials and get identity from access database (.mdb or .accdb)**

```PowerShell
Invoke-OdbcCmd -Dbq 'C:\arbitrary-database.mdb' -Driver '{Microsoft Access Driver (*.mdb, *.accdb)}' "Select @@Identity" -Username 'Arbitrary' -Password 'P@ssw0rd';
```

**Get identity from access database (.mdb or .accdb) by providing ConnectionString**

```PowerShell
$connectionString = 'Driver={Microsoft Access Driver (*.mdb, *.accdb)};Dbq=C:\arbitrary-database.mdb;Uid=Arbitrary;Pwd=P@ssw0rd;';
Invoke-OdbcCmd -ConnectionString $connectionString;
```

For more information concerning ConnectionStrings see [here](https://www.connectionstrings.com/microsoft-access-accdb-odbc-driver/)
