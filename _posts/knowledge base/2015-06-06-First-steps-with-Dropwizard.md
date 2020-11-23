---
layout: post
category: knowledge-base
title: First steps with Dropwizard
date: 06 Jun 2015
tags: RESTful Dropwizard Java development
---

Once at work a friend asked me, if I know dropwizard. I have never heard about it before, so I decided to have a look at it and try it out. Dropwizard is a Java framework for development of high-performance RESTful web services.


To get in touch with dropwizard I went through the [getting started guide](https://www.dropwizard.io/en/latest/getting-started.html). I created a new [repository at GitHub](https://github.com/rufer7/dropwizard-example), where I checked in the source code I wrote while going through the getting started guide.


#### Under the hood

The Dropwizard framework uses the Jetty HTTP library for embedding a HTTP server directly into the project. Dropwizard applications are usually delivered as a FAT-jar, which contain a main method to spin up the embedded HTTP server. The RESTful services developed with Dropwizard are based on [jersey](https://jersey.java.net/) and for JSON serialization and deserialization the framework uses the [Jackson JSON library](https://jersey.java.net/). 
Dropwizard applications support operation tools for metrics, thread dumps, ping and health checks out of the box and are capable of doing 30'000-50'000 requests per second.


#### Project setup

The setup of a Dropwizard project was quite easy. Such an application consists out of the following parts:

* Configuration class
{% gist c62d20a099f7e0b11581 %}
In the configuration class the environment specific parameters are defined. In this case the template message template and the default name. The values of these parameters are defined in a YAML-file (example.yml).

* Configuration file (YAML)
{% gist a0f1834b1744da29ddc2 %}
This file contains the values of the parameters defined in the configuration class.

* Application class
{% gist f7f7466cb76f82bc62e7 %}
Similar to spring boot you have to define an application class, which has to extend the Application class from Dropwizard parametrized with the configuration class. It contains the main method, which runs the HTTP server. In the run method you have to define and register the health checks and resources (Examples of health check and resource classes can be found below).

* Representation class
{% gist cc32aa881386bdeb41e8 %}
This class is optional, but was added to wrap the REST responses into a common top level object, which always contains an id and a data object.

* Resource class
{% gist 0242b89c7f14879df2de %}
The resource class describes the REST resource and is associated with an URI template. The `getExample` method defines a GET endpoint, which serves a response wrapper object containing some data in the content JSON object. The @Timed annotation on the `getExample` method causes that the duration and rate of its invocations is automatically recorded as a Metrics Timer.

There is a possibility to create custom health check classes, which expose health check data to the operation tools.

It's recommended to build Dropwizard application as FAT-jars. How to do that using Maven is described in the [getting started guide](http://www.dropwizard.io/0.9.1/docs/getting-started.html).

For more details have a look at [my example project @GitHub](https://github.com/rufer7/dropwizard-example) and into the [getting started guide](http://www.dropwizard.io/0.9.1/docs/getting-started.html).


#### Conclusion

Throughout this short dive into Dropwizard I noticed that the framework is easy to use and works very well. The getting started guide is well illustrated and contains good descriptions of every part of the application.
Especially impressive was the out of the box operational tools (metrics, thread dump, ping and health check). I didn't do some load test, so I can't place any statement about performance, but as written in the documentation Dropwizard applications should be able to handle 30'000-50'000 requests per second. I think the framework is a good option for implementing RESTful web service i.e. microservices. As well for creating demonstrations or PoC it would be a straight forward approach using Dropwizard.

#### Links

* [My example project @GitHub](https://github.com/rufer7/dropwizard-example)
* [Dropwizard.io](http://www.dropwizard.io)
* [Dropwizard getting started](http://www.dropwizard.io/0.9.1/docs/getting-started.html)
* [Dropwizard user manual](https://www.dropwizard.io/en/latest/)
