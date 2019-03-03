title: RabbitMQ
date: 2015-09-03 22:57:02
tags: [Message Queue, Python]
categories: R&D
---

We need to prepare to scale up our web apps and do the time consuming jobs asynchronously in a stable way. Queue is a good tool to fullfill this requirement.

RabbitMQ fits our needs after investigation, so we try to add it into our apps. 

<!--more-->

Some terms need to mention:

**producer**: A program that sends messages

**consumer**: A program that mostly waits to receive messages.

**queue**:  A buffer that stores messages. It is like a mailbox. Although messages flow through RabbitMQ and your applications, they can be stored only inside a queue. A queue can store as many messages as you like ‒ it's essentially an infinite buffer. Many producers can send messages that go to one queue, many consumers can try to receive data from one queue. 
In RabbitMQ a message can never be sent directly to the queue, it always needs to go through an exchange. 

**exchange**: It receives messages from producers and it pushes them to queues.

exchange types: direct, topic, headers and fanout.


**Note**:

 - Declare a queue to make sure it exists before using it.

 - If we send a message to non-existing location, RabbitMQ will just trash the message. 

 - Before exiting the program we need to make sure the network buffers were flushed and our message was actually delivered to RabbitMQ. We can do it by gently closing the connection.


It is highly recommended to read through the official tutorial:
https://www.rabbitmq.com/getstarted.html

Here is an example making use of the routing example and also enable fair dispatch for multiple workers.

![](/images/pika.png)
![](/images/rabbit.png)
