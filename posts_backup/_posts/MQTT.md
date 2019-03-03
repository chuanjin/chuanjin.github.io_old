title: "MQTT"
date: 2015-03-19 19:42:19
tags: [Message Queue, Python]
categories: R&D
---

# MQTT

{% blockquote [http://mqtt.org] %}
MQTT (MQ Telemetry Transport) is a machine-to-machine (M2M) / "Internet of Things" connectivity protocol. It was designed as an extremely lightweight publish/subscribe messaging transport. It is useful for connections with remote locations where a small code footprint is required and/or network bandwidth is at a premium.
{% endblockquote %}

MQTT is explicitly built for devices with limited resources and is therefore very light on battery. It is designed for unreliable TCP networks or low bandwidth and ideal to run on an embedded device with limited processor or memory resources.

<!--more-->

The idea is that, every client could behave like a subscriber, a publisher or both. Clients do not communicate directly, all the messages should go through the broker, which is the central server. A client subscribes a topic to the broker, just like listening to a channel, whenever there is new data published from any publisher to the topic, the broker will push it to the interested subscribers, the subscriber has no idea who is the publisher of the message, they only care about the message and topic.


## Quality of Service
There are three levels of Quality of Service (QoS) defined in MQTT. The QoS defines how hard the broker/client will try to ensure that a message is received. Higher levels of QoS are more reliable, but involve higher latency and have higher bandwidth requirements.

 - 0: The broker/client will deliver the message once, with no confirmation.
 - 1: The broker/client will deliver the message at least once, with confirmation required.
 - 2: The broker/client will deliver the message exactly once by using a four step handshake.


## Retained Messages

All messages may be set to be retained, by setting a retained flag. This means that the broker will keep the message even after sending it to all current subscribers. If a new subscription is made that matches the topic of the retained message, then the message will be sent to the client immediately. This is useful as a "last known good" mechanism. If a topic is only updated infrequently, then without a retained message, a newly subscribed client may have to wait a long time to receive an update. With a retained message, the client will receive an instant update.


## Clean session / Durable connections

On connection, a client can set the "clean session" flag, which is also known as the "clean start" flag. If clean session is set to false, then the connection is treated as durable. This means that when the client disconnects, any subscriptions it has will remain and any subsequent QoS 1 or 2 messages will be stored until it connects again in the future. If clean session is true, then all subscriptions will be removed for the client when it disconnects.


## Last Will

When a client connects to a broker, it may inform the broker that it has a will message, which will be delivered when the client disconnects unexpectedly. The will message has a topic, QoS and retain status just the same as any other message.


----------

# Mosquitto

[Mosquitto](http://mosquitto.org/) is a famous open source MQTT broker, it is easy to download and install. Below are a few dependency packages might be needed if they are not already existing in you system:

  sudo apt-get update
	sudo apt-get install python-dev gcc g++ make xz-utils libssl-dev uuid-dev

Then you can easily install it

```
	wget http://mosquitto.org/files/source/mosquitto-1.4.tar.gz
	tar xzvf mosquitto-1.4.tar.gz
	cd mosquitto-1.4/
	make
	sudo make install
```

Once installed, you may find mosquitto broker ships with useful command line tools  for testing the pub/sub behavior

![](/images/mosquitto.PNG)

Get more usage info:

    mosquitto_pub --help
    mosquitto_sub --help

You can always check the [documents](http://mosquitto.org/documentation/) for help.

----------

# Paho clients

[Paho](https://eclipse.org/paho) project provides open source clients for MQTT. Let's take python client for instance. To install from source:

	git clone http://git.eclipse.org/gitroot/paho/org.eclipse.paho.mqtt.python.git
	cd org.eclipse.paho.mqtt.python.git
	sudo python setup.py install

A very basic publisher publishes random data every 2 seconds

```python
	import time
	import random
	import paho.mqtt.client as mqtt

	PORT=1883
	HOST='localhost'

	def mqttHandler():
	    mqttc.connect(HOST, PORT)
	    while True:
	        status = random.randint(1,100)
	        print("Sending " + str(status))
	        mqttc.publish("example/basic", payload=status, retain=True)
	        time.sleep(2)

	if __name__ == '__main__':
	    mqttc = mqtt.Client()
	    mqttHandler()
```

A very simple subscriber is listening the topic


```python

	import paho.mqtt.client as mqtt

	PORT=1883
	HOST='localhost'

	def on_message(mosq, userdata, msg):
	    print("Got topic: " + msg.topic + ", message: " + msg.payload.decode("utf-8"))

	def mqttHandler():
	    mqttc.connect(HOST, PORT)
	    mqttc.subscribe('example/basic')
	    while True:
	        mqttc.loop()

	if __name__ == '__main__':
	    mqttc = mqtt.Client()
	    mqttc.on_message = on_message
	    mqttHandler()
```

You need to have you mosquitto broker up and running on you local machine.
![](/images/basic.PNG)
