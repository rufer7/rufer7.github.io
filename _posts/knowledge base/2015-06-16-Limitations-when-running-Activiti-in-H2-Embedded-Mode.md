---
layout: post
category: knowledge-base
title: Limitations when running Activiti in H2 Embedded Mode
date: 16 Jun 2015
tags: Activiti development
---

While playing around with the docker image [eternnoir/activiti](https://registry.hub.docker.com/u/eternnoir/activiti/) I had some troubles accessing deployments, process instances and other data created in activiti explorer over the REST endpoint. It took me some time to find out why the data from explorer was not accessible over REST.
If nothing else specified activiti runs with an embedded H2 database. For playing around and trying out I supposed running activiti with the H2 embedded database would be fine. This assumption was wrong for my case. I wanted to create and deploy a process with activiti explorer and then start it over the REST api. The REST api and the activiti explorer are two different war files, which will be deployed on a websever (i.e. Tomcat). Here comes the problem. When running acitivi in H2 embedded mode the REST api service and the activiti explorer will have their own H2 database instance with different data stored in it. The reason for that behaviour is, that H2 database in embedded mode only allows one connection at the same time.
To test my case I had to connect both services to an external mysql database. The docker image I used allowed to connect the activiti container to a mysql container (For more details have a look at the [manual](https://github.com/eternnoir/activiti#linking-to-mysql-container)). After connecting activiti with mysql I could access the processes designed in activiti explorer over the REST api.