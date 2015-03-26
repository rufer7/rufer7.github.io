---
layout: post
category: knowledge-base
title: AMQP Integration with spring integration gateways
date: dd MMM YYYY
tags: Java spring spring-integration AMQP RabbitMQ
---

Excerpt


Describe the integration within JUnit tests and "Configuration-Tests"/"Messaging Integration tests" -> Add another "consumer" to the chain (at the end) ant test there the input (message)
Text (amqp-sample + Code snippets (Gists)

IMPORTANT: Mention bug with transformers: If you have to transformers for one channel (i.e. one for logging and one for sending to AMQP), spring makes a loadbalancing

    <int:channel id="sampleRequestChannel"/>
    <int:gateway id="sampleGateway" service-interface="full.qualified.interface.name" default-request-channel="sampleRequestChannel"/>
    <int:transformer input-channel="sampleRequestChannel" output-channel="sampleAMQPRequestChannel" expression="payload"/>

    <int:transformer input-channel="sampleRequestChannel" output-channel="consoleOut" expression="'Received: ' + payload"/>
    <int-stream:stdout-channel-adapter id="consoleOut" append-newline="true"/>