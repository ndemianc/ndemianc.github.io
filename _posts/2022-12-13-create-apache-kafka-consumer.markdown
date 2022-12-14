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

1. Open a new terminal and navigate to the directory where Apache Kafka is installed.
2. Run the following command to start the Apache Kafka server:

```
bin/kafka-server-start.sh config/server.properties
```

3. Open another terminal and navigate to the directory where Apache Kafka is installed.
4. Run the following command to create a new topic called "my-topic":

```
bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic my-topic
```

5. Run the following command to start a consumer that listens to the "my-topic" topic:

```
bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic my-topic --from-beginning
```

This will start a consumer that listens to the "my-topic" topic and prints any messages that are published to that topic to the terminal. You can then publish messages to the "my-topic" topic using a Kafka producer, and the consumer will receive and print those messages.

![Kafka]({{site.baseurl}}/images/apache-kafka.jpg)
*Image from [https://www.oreilly.com/](https://www.oreilly.com/library/view/kafka-the-definitive/9781491936153/ch04.html#T1_overflow_nomessage)*
