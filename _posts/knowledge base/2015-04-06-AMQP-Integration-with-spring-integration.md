---
layout: post
category: knowledge-base
title: AMQP Integration with spring integration
date: 06 Apr 2015
tags: Java spring spring-integration AMQP RabbitMQ
---

This blog post gives a short overview about the integration of the AMQP based message queue [rabbitMQ](https://www.rabbitmq.com) with a spring application by using spring integration. The post is illustrated with some sample code- and configuration-snippets.


[Spring integration](http://projects.spring.io/spring-integration) is one of the projects developed and maintained by Pivotal Software. It's a great project, which simplifies integration of different protocols and it's implementations. Spring integration supports the well-known Enterprise integration patterns.
The integration with RabbitMQ shows the benefits by using spring integration. One of them is the abstraction of messages with the spring integration messages, so that the messages are completely decoupled from the underlying message infrastructure.
To get an overview about the integration with rabbitMQ let's dive into the sample.


#### Sample configuration

{% gist 8686fcf28e5d4e10b552 %}

The comments split the configuration into logical parts. We will now have a step-by-step look at these parts.

The infrastructure part contains the following definitions

* connection factory (Manages the connection to the rabbitMQ-instance
* rabbit-template (Used for sending the messages to the queue)
* rabbit-admin (Manages exchanges, queues and bindings)

Next the logging-channel-adapter is defined, which will log the messages to the console followed by two beans (Error handler and header enricher), which will be explained in the sections below.

In the incoming-section a queue is bound to the fanout exchange for incoming messages. The inbound-channel-adapter consumes the messages from the queue and redirects them to the `rawInputChannel`. To enforce spring to not remove custom request headers the `mapped-request-headers` have to be set (In this sample all custom request headers are allowed with `*`). To transform the byte-payload to String the default object to String transformer is used. Last but not least the service-activator is defined. The service-activator by default calls the only public method of the referenced bean.

Now we come to the last part of the configuration, the outgoing-section. First a gateway is defined, which references an interface that will be used to send messages to the queue. All messages sent by the referenced inteface will be redirected to the `rawToAMQP`-channel. If a message is sent by the `sendSomething`-method a static custom header (i.e. api-version) will be added to the request. The chain followed by the gateway takes the messages from the `rawToAMQP`-channel. For every message first the `object-to-json`-transformer, which transforms the java-objects in the message body to JSON, and after that the `addCustomHeaders`-method of the referenced header enricher is called. With chains it's possible to execute several transformers, filters, header enrichers, etc in a defined order without defining separate input- and output-channels for every component. The output of the chain will be sent to the defined amqp-exchange by the `outbound-channel-adapter`.


#### Error handler

The following code snippet shows the error handler used by the configuration. Error handlers have to implement the ErrorHandler-interface.

{% gist b06740900d03970fc62f %}

If an error occurs in the `inbound-channel-adapter` the `handleError`-method will be called. In this case an `AmqpRejectAndDontRequeueException` will be thrown. As the name already says this exception will reject the message without requeuing it.


#### Header enricher

For enrichment of headers with custom static or non-static headers a custom header enricher can be implemented. Below a sample implementation.

{% gist 3e691a15ed77f96f7282 %}

Such a custom header enricher class takes the message as parameter and must return a Map with the headers, which should be added to the message.


#### Message Handler

To handle incoming spring integration messages a message handler class has to be provided. Message handlers either have to implement the MessageHandler-interface or the method to be called has to be defined in the configuration of the service activator by setting the `method`-attribute accordingly. In both cases the method, which handles the message has to be `void` and has to take a spring integration message as parameter.  

{% gist 5fcb93ca7217dd1fd5cb %}


#### Gateway

Sending messages to the spring integration channels is done interfaces, which are referenced by spring integration gateways. Such an interface defines the send-methods, where headers and payload are defined as method parameters.

{% gist ba8cac16fbde5cfd209f %}

The interface can then be used in any service by injecting it. You don't have to provide an implementation. Spring will use the GatewayProxyFactoryBean to inject basic code to the gateway, which allows reading of string based messages. 


#### Troubleshooting

When working on the integration with [rabbitMQ](https://www.rabbitmq.com) I first configured two transformers. One of them took the incoming message and sent only the payload to the output channel and the other one, which logged the message payload to the console. Below you can see an excerpt of the configuration. 

    <int:channel id="sampleRequestChannel"/>
    <int:gateway id="sampleGateway"
            service-interface="full.qualified.interface.name"
            default-request-channel="sampleRequestChannel"/>
    <int:transformer input-channel="sampleRequestChannel"
            output-channel="sampleAMQPRequestChannel"
            expression="payload"/>

    <int-stream:stdout-channel-adapter id="consoleOut"
            append-newline="true"/>
    <int:transformer input-channel="sampleRequestChannel"
            output-channel="consoleOut"
            expression="'Received: ' + payload"/>

The problem here is, that both of the transformers listen to the same channel. If you have two transformers listening to the same channel spring makes a loadbalancing. If you want to append both transformers for every message working with spring integration chains will be the solution. For more details have a look at the [documentation](http://docs.spring.io/spring-integration/docs/2.0.0.M3/spring-integration-reference/html/chain.html).