---
layout: post
title:  "DIY Smarthome with ESP8266 and Node-Red"
date:   2020-10-16 22:17:00 +0100
categories: jekyll update
tags: raspberrypi arduino ESP8266
---
# Start with the Sensors
To build a sensor dashboard accessible from the internet, the first step is getting your sensor connected to the internet. This can be done with a microcontroller like the wifi board in the picture below ([ESP8266 NodeMCU](https://de.wikipedia.org/wiki/ESP8266)):
<figure>
<img src="/assets/images/nodemcu.jpg" alt="nodemcu" width="30%">
<figcaption>A NodeMCU ESP8266 Wifi Board</figcaption>
</figure>

Once you've wired your sensor to the board, you can program the board to read these sensor values and send over the internet to a place where your dashboard can access it. Using the [MQTT](https://de.wikipedia.org/wiki/MQTT)) protocol, you can publish data at regular intervals to a so-called MQTT broker, which is a server that receives messages published by sensors and forwards them onward to any programs that have subscribed to the topic the message was published to. You can run an MQTT server on a Raspberry Pi using [Mosquitto](https://mosquitto.org/) or use free online services like [cloudMQTT.com](https://www.cloudmqtt.com/).
<figure>
<img src="/assets/images/fridgeSensor.jpeg" alt="fridge" width="75%">
<figcaption>This ESP8266 is wired to a magnetic door switch, which sends a signal each time it is opened.</figcaption>
</figure>

Set up a few different sensors around the house connected to NodeMCUs, and program them all to publish their readings to your MQTT broker.

# Receiving Sensor Data, Generating the Dashboard
With the open-source low-code programming suite [Nodered](https://nodered.org/) running on a server of your choice, you can easily subscribe to an unlimited number of MQTT topics and perform actions based on the input you receive. 
<figure>
<img src="/assets/images/noderedAdmin.png" alt="nodered" width="100%">
<figcaption>Sample MQTT input flows in Nodered</figcaption>
</figure>

After installing the `node-red-dashboard` package for Nodered, you can implement all sorts of charts and gauges on a website for displaying the values from your wifi sensors.
<figure>
<img src="/assets/images/smarthomeDashboard.png" alt="sh" width="100%">
<figcaption>Brian's Nodered Sensor Dashboard</figcaption>
</figure>
