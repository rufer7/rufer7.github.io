---
layout: post
category: knowledge-base
title: Configuration properties meta-data support in IntelliJ
date: 06 Apr 2015
tags: Java spring IntelliJ IDEA JetBrains
---

In the [JetBrains](https://www.jetbrains.com) webinar about `Spring Boot Support in IntelliJ IDEA 14.1` an interesting functionality of IntelliJ IDEA was presented. Since version 14.1 IntelliJ supports "code completion" and contextual help for configuration properties when working with `application.properties`-files in spring boot context.


Spring boot jars contain meta-data files located inside `META-INF` that provide details for configuration properties. These meta-data files are json-files named `spring-configuration-metadata.json`. The "code completion" for configuration properties in IntelliJ is based on these meta-data files placed under `META-INF`.

Every spring boot based jar that supports configuration properties can provide such a meta-data file called `additional-spring-configuration-metadata.json`. The additional meta-data file will then be automatically merged to the main meta-data file by the annotation processor and will be resolved by IntelliJ for the "code completion" in `application.properties`.

The following snippet shows an example of such an additional meta-data file.

{% gist 099292083672d5e203f1 %}

For more details about the configuration meta-data have a look at the spring boot documentation ([Appendix B Configuration meta-data](http://docs.spring.io/spring-boot/docs/current/reference/html/configuration-metadata.html))

For an example use of the "code completion" functionality in IntelliJ have a look at the recorded JetBrains webinar [@Youtube](https://www.youtube.com/watch?v=IUb52gHQGLE) from 18:30.


#### Links

Below some links related to the webinar about `Spring Boot Support in IntelliJ IDEA 14.1`

* [Recorded JetBrains webinar @Youtube](https://www.youtube.com/watch?v=IUb52gHQGLE)
* [Sample code to JetBrains webinar](https://github.com/snicoll-demos/spring-boot-intellij-idea-webinar)