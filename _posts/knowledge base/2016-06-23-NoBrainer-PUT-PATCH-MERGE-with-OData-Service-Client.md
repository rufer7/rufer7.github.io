---
layout: post
category: knowledge-base
title: Apply Commit from one Repository to another
date: 23 Jun 2016
tags: .NET C# OData
---

Visual Studio supports the generation of data service clients (Service references) for OData services. A data service client is a .NET class that contains methods for accessing the OData service and gets generated based on the metadata provided by the OData service. The client acts as a proxy and translates the method calls into HTTP requests.

Mike Wasson describes in his blog post [Calling an OData Service From a .NET Client (C#)](http://www.asp.net/web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client) how to generate and use such a data service client.

When updating objects using the data service client the client by default sends a HTTP MERGE request after calling `container.SaveChanges()`.

If desired the default behaviour can be easily changed. To do PUT or PATCH requests instead of MERGE the `SaveChangesDefaultOptions` have to be changed as shown below.

#### PUT
```C#
<code>container.SaveChangesDefaultOptions = System.Data.Services.Client.SaveChangesOptions.ReplaceOnUpdate;
```

#### PATCH
```C#
container.SaveChangesDefaultOptions = System.Data.Services.Client.SaveChangesOptions.PatchOnUpdate;
```
