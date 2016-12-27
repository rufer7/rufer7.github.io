---
layout: post
category: knowledge-base
title: HOWTO Set Cookie Header on DefaultRequestHeaders of HttpClient
date: 27 Dec 2016
tags: .NET C# HttpClient
---

For one of our customers we had to implement Cookie handling for authentication purposes. This means reading the session token out of the `Set-Cookie` header and send the session token in the `Cookie` header of every request. When using the HttpClient from System.Net.Http there are two possibilites to do that. Either by passing a `HttpClientHandler` with a `CookieContainer` to the HttpClient, which then automatically handles cookies (See [here](http://stackoverflow.com/a/12374486/2796003)), or by manually handle them. As we create a new instance of the HttpClient in our wrapper for every request, we had to go for the 2nd option.

We then tried to manually add the `Cookie` header with the session token as value to the `DefaultRequestHeaders` of the HttpClient as follows.

```CSharp
using (var httpClient = new HttpClient())
{
var uri = new Uri("http://www.example.com");
httpClient.BaseAddress = uri;
httpClient.DefaultRequestHeaders.Add("Cookie", "auth=ArbitrarySessionToken");
var response = httpClient.GetAsync(uri).Result;
}
```

Adding the `Cookie` header to the `DefaultRequestHeaders` worked fine without any exception. However unexpectedly the `Cookie` header got ignored by the HttpClient and was not present in the request. We searched in the internet for a solution to solve this problem and found the [answer](http://stackoverflow.com/questions/12373738/how-do-i-set-a-cookie-on-httpclients-httprequestmessage/13287224#13287224) on StackOverflow. The solution was to pass a `HttpClientHandler` with the `UseCookies` property set to false to the constructor of the HttpClient.

```CSharp
using (var httpClient = new HttpClient(new HttpClientHandler { UseCookies = false }))
{
var uri = new Uri("http://www.example.com");
httpClient.BaseAddress = uri;
httpClient.DefaultRequestHeaders.Add("Cookie", "auth=ArbitrarySessionToken");
var response = httpClient.GetAsync(uri).Result;
}
```
