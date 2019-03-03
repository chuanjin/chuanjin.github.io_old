title: MQTT with websockets support
date: 2015-12-07 09:38:41
tags: [Message Queue]
categories: R&D
---


Since version 1.4, mosquitto MQTT broker starts to support websockets natively. Now it is a try out for this great new feature.

The websocket support is not enabled by default, so we have to fetch the source code firstly and update one line in file ** config.mk **

<!--more-->

```
    WITH_WEBSOCKETS:=no
```

change it to ** yes **, then you can compile and install it.

```
    make
    sudo make install
```

In case you got dependency errors, install the package as below.

```
    apt-get install libc-ares-dev libwebsockets-dev libssl-dev uuid-dev
```

Try to start mosquitto broker with command **mosquitto** to see if it is working properly.
Then we need a customized mosquitto config file, let's call it **mqtt.conf** 


```
    listener 1883
    protocol mqtt
    
    listener 1884
    protocol websockets
```


Now when we start with the command ** mosquitto -c mqtt.conf **, you should see something like this:
![](/images/broker_start.png)

It is time for the websocket coming in. We need a mqtt javascript client here called ** mqttws31.js ** , available from [Paho](https://eclipse.org/paho)
An example code would look like:


```
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01//EN">
    
    <html>
    <head>
        <title>Mosquitto Websockets</title>
        <script src="jquery.js" type="text/javascript"></script>
        <script src="mqttws31.js" type="text/javascript"></script>
        <script type="text/javascript">
        var mqtt;
        var reconnectTimeout = 2000;
        var port = 1884;
        var host = "127.0.0.1"
        var topic = "+/#"
    
        function MQTTconnect() {
        mqtt = new Paho.MQTT.Client(
                host,
                port,
                "client_X") ;
        var options = {
            timeout: 3,
            cleanSession: false,
            onSuccess: onConnect,
            onFailure: function (message) {
                $('#status').val("Connection failed: " + message.errorMessage + "Retrying");
                setTimeout(MQTTconnect, reconnectTimeout);
            }
        };
    
        mqtt.onConnectionLost = onConnectionLost;
        mqtt.onMessageArrived = onMessageArrived;
    
        mqtt.connect(options);
        }
    
        function onConnect() {
        $('#status').val('Connected to ' + host + ':' + port);
        // Connection succeeded; subscribe to our topic
        mqtt.subscribe(topic, {qos: 0});
        }
    
        function onConnectionLost(response) {
        setTimeout(MQTTconnect, reconnectTimeout);
        $('#status').val("connection lost: " + responseObject.errorMessage + ". Reconnecting");
    
        };
    
        function onMessageArrived(message) {
    
        var topic = message.destinationName;
        var payload = message.payloadString;
    
        $('#ws').prepend('<li>' + topic + ' = ' + payload + '<\/li>');
        };
    
    
        $(document).ready(function() {
        MQTTconnect();
        });
    
        </script>
    </head>
    
    <body>
        <h1>Mosquitto Websockets</h1>
        <div>
            <div>
                Status: <input type='text' id='status' size="80" disabled="disabled">
            </div>
            <ul id='ws'>
            </ul>
        </div>
    </body>
    </html>

```

Initially it looks like

![](/images/web1.png)

If we start to send some messages from command like, we will get the data coming via mqtt through mosquitto broker and then via websocket published to js client.

![](/images/pubsub.png)
![](/images/web2.png)
