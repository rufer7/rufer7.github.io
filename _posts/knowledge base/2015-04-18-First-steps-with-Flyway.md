---
layout: post
category: knowledge-base
title: First steps with Flyway
date: 18 Apr 2015
tags: database migration Flyway maven development
---

After reading a blog post about the database migration tool [Flyway](http://flywaydb.org) on [jaxenter](http://jaxenter.de) I decided to play around with it in the context of a little sample project. The sample project shows the usage of the flyway maven plugin in combination with a h2 database.


#### About Flyway

<div class="inline-img-right">
    <img src="{{ site.url }}/assets/logos/flyway_logo.png" alt="Flyway logo"/>
</div>

A short introduction about database migrations can be found [here](https://flywaydb.org/getstarted/why.html). To get some basic information about Flyway and how it works have a look at [How Flyway works @Flywaydb.org](http://flywaydb.org/getstarted/how.html).

For more details have a look at the [Flyway documentation](https://flywaydb.org/documentation)


#### Getting started

To set up the sample project I had a look into the [Get started with maven guide](https://flywaydb.org/getstarted/firststeps/maven.html). With the information provided there the setup was straight forward. The configuration of the maven plugin is pretty intelligible and the configuration tags are documented well.

Below you can see the pom-file of my sample project

{% gist 6fa60555ce53ddaa0e9c %}

The database migration files by default have to follow the pattern `V{VERSION_NUMBER}_{NAME_OF_THE_FILE}.sql` and have to be placed in the migration directory `src/main/resources/db/migration`.

The sources of the sample project can be found on my [GitHub-Account](https://github.com/rufer7/flyway-example).


#### Flyway and spring boot

Spring boot supports flyway database migrations by running them automatically on startup. For more information have a look at the [Spring boot documentation](http://docs.spring.io/spring-boot/docs/current/reference/htmlsingle).


#### Conclusion

The configuration of the maven plugin was very straight forward and the plugin worked well for my little sample. On the flyway website you can find some get started tutorials for command line, java API, Maven, Gradle, Ant and SBT. These tutorials are good starting point for everybody who wants to check out the basic functionalities of Flyway.

Furthermore the flyway website provides a lot of information around flyway, which are easy to find thanks to a clear structure.


#### Links

* [Flyway documentation](https://flywaydb.org/documentation)
* [Existing DB setup](https://flywaydb.org/documentation/existing.html)
* [Spring boot integration of flyway](http://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#howto-execute-flyway-database-migrations-on-startup)