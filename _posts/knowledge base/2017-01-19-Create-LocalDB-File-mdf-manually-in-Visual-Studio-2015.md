---
layout: post
category: knowledge-base
title: HOWTO Create LocalDB File (.mdf) manually in Visual Studio 2015
date: 19 Jan 2017
tags: SQL VisualStudio
---

If you are using **LocalDB** and want to create an empty database you should perform the following steps.

1. Go to Visual Studio `Server Explorer` | `Data Connections`
1. Select `Add Connection` from the context menu
1. Change `Data Source` to `Microsoft SQL Server Database File` (i.e. LocalDB)
1. Set the `Database file name` by entering a database name and path that corresponds to the name in the `web.config`/`app.config` connectionstring.
  Replace `|DataDirectory|` with path to the place the database file should be created at (i.e. `App_Data`)
1. Select `Advanced` and set the properties according to the following example connection string

  ```
  Data Source=(localdb)\v11.0; Initial Catalog=Arbitrary; Integrated Security=True; MultipleActiveResultSets=True; AttachDbFilename=C:\PATH\TO\Arbitrary.mdf
  ```
