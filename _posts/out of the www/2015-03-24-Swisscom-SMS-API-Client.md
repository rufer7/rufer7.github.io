---
layout: post
category: out-of-the-www
title: Swisscom SMS-API-Client
date: 24 Mar 2015
tags: Java API RESTful library
---

Today the v1.0 of the [swisscom-sms-api-client](https://github.com/rufer7/swisscom-sms-api-client) was released and is now available at [Maven Central Repository](http://search.maven.org/#artifactdetails%7Cbe.rufer.swisscom.sms%7Capi-client%7C1.0%7Cjar)! The Swisscom SMS-API client project is an open source library for easy use of the [Swisscom SMS-API](https://developer.swisscom.com/documentation/api/products/SMS%20Messaging) in Java.


The idea to write this library appeared to me after playing around with the Swisscom SMS-API. The main goals of implementing this API-client were on the one side allowing an easy integration of the API into java applications and on the other side to have a reference project for a first contribution to the [Maven Central](http://search.maven.org/) repository.


#### How to use

To include the library into your maven project you have to add the following dependency section to your pom.xml

    <dependency>
        <groupId>be.rufer.swisscom.sms</groupId>
        <artifactId>api-client</artifactId>
        <version>1.0</version>
    </dependency>


Using the library is straight forward as you can see in the code snippet below

{% gist 245d6c4044b4bc3160d9 %}



It was interesting going through all the necessary steps for a deployment of an artifact to the central repository. At this point I'd like to mention the good and helpful documentation of [Maven Central](http://central.sonatype.org/pages/producers.html). Without this documentation the release process had been much more time consuming.

Special thanks goes to Konrad Lykowski for the code review and the valuable feedback.


#### Links to swisscom-sms-api-client project

* [Maven Central](http://search.maven.org/#artifactdetails%7Cbe.rufer.swisscom.sms%7Capi-client%7C1.0%7Cjar)
* [GitHub](https://github.com/rufer7/swisscom-sms-api-client)