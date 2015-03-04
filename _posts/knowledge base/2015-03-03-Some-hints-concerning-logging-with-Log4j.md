---
layout: post
category: knowledge-base
title: Some hints concerning logging with Log4j
date: 03 Mar 2015
tags: Java logging Log4j
---

This blog post treats some useful information concerning logging with the logging framework Log4j version 2. The post covers the different log levels, the configuration for a rolling file appender and some information regarding performance.


<div class="img-default">
    <img src="{{ site.url }}/assets/logos/log4j_logo.jpg" alt="Log4j-Logo"/>
</div>

The logging framework Log4j is a Java Open Source project, which is part of the logging project of the [Apache Software Foundation}(http://www.apache.org/). It's one of the most used logging frameworks.


#### Log levels

Log4j provides different log levels, which are listed and shortly described below

Level | Description
:----------- | :-----------
`TRACE` | Detailed logging i.e. for comments
`DEBUG` | Debug logs for analyzing and troubleshooting bugs
`INFO` | Common information about application execution like "Execution started",..
`WARN` | Logging unexpected occurrences
`ERROR` | Exception logging (i.e. catched exceptions)
`FATAL` | Critical errors and program termination


#### Configure rolling file appender

A common use case is configuring the logging framework to log some specific log messages or even all log messages to a file. With Log4j this can be done by adding the following configuration to the `log4j.properties` file
{% gist bf26f950970eb1fc95e7 %}

The first line sets the log level for the package `org.web.rufer.sample` to `DEBUG` and sets the log appender. Lines 4 to 9 configure the log appender named `ROLLINGFILEAPPENDER`. Besides the path and name of the file there are as well properties provided to set the maximal file size, maximal file backup count and of course the layout of the log messages.


#### Performance optimization

To optimize logging performance it's advisable to use the methods, which take a string with placeholders and a list of objects as parameters (see `Sample 2` and `Sample 3`). The advantage to use the placeholder variant instead of method with string parameter like in `Sample 1` is, that the toString()-method of object arguments will only be evaluated, if the corresponding log level is activated. In `Sample 1` the String will be built in every case. If you have a lot of debug logs with rich toString-logic this could be an issue.
{% gist 10ee4cf3aa31c5de3b7e %}

For more information about Log4j consult the [Log4j manual](http://logging.apache.org/log4j/2.x/manual/index.html)