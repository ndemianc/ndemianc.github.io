---
layout: post
title:  Create Apache Kafka Consumer
description:
date:   2022-12-13 00:31:46.882708 -0500
author: sdemian
image:  '/images/working-with-kafka-consumers.jpg'
tags:   [kafka, technology, java]
tags_color: '#477690'
---
To create an Apache Kafka consumer, you will need to first install Apache Kafka on your system, if you haven't already done so. You can download Apache Kafka from the official website (https://kafka.apache.org/downloads). Once you have installed Apache Kafka, you can create a consumer by following these steps:

- Open a new terminal and navigate to the directory where Apache Kafka is installed.
- Run the following command to start the Apache Kafka server:

{% highlight sh %}
bin/kafka-server-start config/server.properties
{% endhighlight %}

- Open another terminal and navigate to the directory where Apache Kafka is installed.
- Run the following command to create a new topic called "my-topic":

{% highlight sh %}
bin/kafka-topics --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic my-topic
{% endhighlight %}

- Run the following command to start a consumer that listens to the "my-topic" topic:

{% highlight sh %}
bin/kafka-console-consumer --bootstrap-server localhost:9092 --topic my-topic --from-beginning
{% endhighlight %}

This will start a consumer that listens to the "my-topic" topic and prints any messages that are published to that topic to the terminal. You can then publish messages to the "my-topic" topic using a Kafka producer, and the consumer will receive and print those messages.

![Kafka]({{site.baseurl}}/images/apache-kafka.jpg)
*Image from [https://www.oreilly.com/](https://www.oreilly.com/library/view/kafka-the-definitive/9781491936153/ch04.html#T1_overflow_nomessage)*
