---
layout: post
category: out-of-the-www
title: Swissunihockey game schedule PDF generator
date: 20 Jul 2015
tags: swissunihockey sports Java ical4j PDFBox
---

On the new website of [swissunihockey](http://www.swissunihockey.ch) there is no possibility to get an overview of all games of a team represented on one page. Based on that I decided to write an application that allows to generate a PDF document displaying the game schedule of a team.


#### Solution

First I had to study the [swissunihockey API v2](https://api-v2.swissunihockey.ch/api/doc). The fact that the swissunihockey API is not designed RESTful made the challenge a bit more difficult. For example getting a club or a team by `id` is not possible, so I had to provide some workarounds to solve these problems (i.e. static map in service that holds the mappings between `id` and `name` for every club).

To get a proper formatted game schedule of a specific team I decided to consume the game schedule in ical format (`/calendar` endpoint). I started implementing the API client that consumes the [swissunihockey API v2](https://api-v2.swissunihockey.ch/api/doc) and serves the data in the desired format. The ical data from the `/calendar` endpoint will be transformed into a Calendar object provided by the [ical4j library](http://ical4j.github.io/about/).

After finishing the API client I continued with the PDFGenerator, which is responsible to process the Calendar data and write it to a new PDF document. The PDF files are generated with [Apache PDFBox](http://pdfbox.apache.org/). Before implementing the frontend I had to implement a service that gets data from the API client and creates the PDF document and a controller exposing an endpoint to consume the generated PDF document.

The frontend is built with [Ionic](http://ionicframework.com/), an AngularJS based front-end SDK. Because direct requests to the swissunihockey API from the javascript are not allowed (CORS) I set up a [zuul](https://github.com/Netflix/zuul/wiki) proxy that proxies all requests to the swissunihockey API.


#### Conclusion

The application I wrote is a spring boot application using the following libraries:

* Ionic (Frotend library)
* spring-cloud-starter-zuul (For enabling CORS)
* ical4j (For processing ical data)
* PDFBox (For PDF creation)


The application can be visited [here](http://swissunihockey-pdf-generator.rufer.be)

The source code of the application is freely available on [GitHub](https://github.com/rufer7/swissunihockey-game-schedule-pdf-creator)