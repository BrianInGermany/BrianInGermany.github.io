---
layout: post
title:  "Power-Charge Your Nodered Data with Grafana and InfluxDB"
description: "Store your data simply and visualize the crap out of it"
date:   2020-10-20 20:37:00 +0100
categories: jekyll update
tags: raspberrypi grafana nodered influxdb
header:
  teaser: "/assets/images/grafanaDash.png"
---

# You should be saving to InfluxDB

You're saving sensor readings to text files? There is a more efficient and simple way to do it. InfluxDB is an open-source database made especially for time-series data like sensor readings. And the great thing is, you can write to it directly from a Nodered node. 
<figure>
<img src="/assets/images/mqttFlow.png" alt="nodered_flow" width="75%">
<figcaption>This flow writes incoming MQTT data directly to InfluxDB</figcaption>
</figure>

It's as easy as `cd`ing into your `.node-red` directory and installing the InfluxDB Nodered package: `npm install node-red-contrib-influxdb`. Once InfluxDB nodes appear in your node selector panel, just link them up to your desired output and configure.
<figure>
<img src="/assets/images/influxDBnode.png" alt="influx_node" width="75%">
<figcaption>Configuring the InfluxDB Nodered node</figcaption>
</figure>

Of course, you'll need to have installed InfluxDB on your server first! To do that, check out this [great tutorial](https://simonhearne.com/2020/pi-influx-grafana/) by [Simon Hearne](https://github.com/simonhearne). It's a nice step-by-step, and when you're done you will also have installed [Grafana](https://grafana.com/), which means you'll be ready to start inspecting your DB data, too!

# Grafana

As soon as you've configured the InfluxDB credentials and DB name in Nodered (providing your flow has received any data, in my case via the MQTT-in node), you will be able to access these so-called InfluxDB measurements in the Grafana panel setup page. Remember, first add the datasource to Grafana like this, under the datasources tab:

<img src="/assets/images/addDatasource.png" alt="add_datasource" width="25%">

Finally, go to your Grafana dashboard, add a new panel, and select your measurement from the `select measurement` dropdown field, which autopopulates from InfluxDB if there is data in it:


<img src="/assets/images/load_influx_measurement.png" alt="measurement" width="75%">

As soon as you click somewhere else on the screen the datapoints will appear on the chart! If you don't like the dots and prefer a continuous line just choose the setting `Stacking and Null Value` - `Null Value` -> `connected` here:


<img src="/assets/images/connectedGRafana.png" alt="connected" width="25%">

And if you want multiple lines on one graph, just press the `+ Query` sign to add a new query:

<img src="/assets/images/plusQuery.png" alt="plusquery" width="50%">