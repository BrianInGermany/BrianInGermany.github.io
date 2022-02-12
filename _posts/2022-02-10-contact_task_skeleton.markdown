---
layout: post
title:  "X-Ray Your Team with Graphviz"
description: "Use a Contact-Task Graph to Trace Your Communication Backbone"
date:   2022-02-10 21:51:00 +0100
categories: jekyll update
tags: thinking-aids graphviz
header:
  teaser: "/assets/images/contact_skeleton.png"
---
<img src="/assets/images/xray.jpg" alt="hand_skeleton">
A team's lines of communication make up its organizational backbone for getting tasks done.
By mapping your contacts to your most important tasks and topics, you can visualize how information flows between you and team members, and better explain to others your role in the project.

## Enter DOT Graph Language and Graphviz

The [DOT graph language](https://graphviz.org/doc/info/lang.html) and [Graphviz](https://graphviz.org) provide a protocol for recording network-structured relationships between elements. 

In its simplest form, DOT provides a framework for connecting nodes, denoted by single words, with edges, denoted by the double dash (`--`). A simple undirected graph could look like this:

```dot
graph graph1 {
	hearing -- sight;  
	sight -- taste;  
	taste -- hearing;  
	hearing -- touch;  
	touch -- taste;
}
```

<figure>
<img src="/assets/images/simple_network.png" alt="simple_network">
<figcaption>a simple network with DOT</figcaption>
</figure>

## The Contact-Task Graph

To go from a simple network graph to a contact-task graph, we need a network plotter that will enable a radial rendering of several (three) layers of nodes, represented in concentric circles. For this, DOT's `twopi` layout comes in handy.

Along with some additional node coloring and font settings metadata, the raw data of the contact graph is stored in the below text file. Note that the metadata is set at the beginning, and also includes the specification of the root node. The ring levels of nodes are defined by the separate mappings of the root node to the contact-person nodes, as well as the contact-person nodes to the task nodes. For clarity, the edge lines are shown in alternating rainbow colors. Don't worry about the numbers with hashtags, those are just a notation for a more exact color.

Also, if your nodes get too close together because you have so many, try adjusting the `ranksep` value higher.

```dot
graph contacts_tasks {
	fontname=Arial;
	layout=twopi; 
	graph [ranksep=3] [overlap=true][root=Brian];
	edge [penwidth=1 color="#000000"]
	node [fontname=Bahnschrift]
	node [style="filled" fontsize=15 penwidth=0 fillcolor="#c96463"]
	Brian -- {
		node [style="filled" fontsize= 10 penwidth=0 fillcolor="#d9c762"]
		Adam
		Brad
		Chris
		Donald
		Edward
		Frank
		Gina
		Haley
		Ida
		Jennifer
		Kyle

	}
	node [style="filled" fontsize= 15 penwidth=0 fillcolor="#d9c762"]
	edge [color=red]
	Adam -- {
		node [style="filled" fontsize= 10 penwidth=0 fillcolor="#dbd8c8"]
		folk_music
		tech
		writing
		linguistics
		public_speaking
		retro_computing
		conversational_ai
		jamulus
				


	}
	edge [color=orange]
	Brad -- {
		node [style="filled" fontsize= 10 penwidth=0 fillcolor="#dbd8c8"]
		folk_music
		raspberrypi
		guitar
		jamulus
		linguistics
		public_speaking
	}
	edge [color=green]
	Chris -- {
		node [style="filled" fontsize= 10 penwidth=0 fillcolor="#dbd8c8"]
		writing
		linguistics
	}
	edge [color=blue]
	Donald -- {
		node [style="filled" fontsize= 10 penwidth=0 fillcolor="#dbd8c8"]
		tech
		python
		nodered
	}
	edge [color=purple]
	Edward-- {
		node [style="filled" fontsize= 10 penwidth=0 fillcolor="#dbd8c8"]
		nodered
		tech
	}
	edge [color=red]
	Frank -- {
		node [style="filled" fontsize= 10 penwidth=0 fillcolor="#dbd8c8"]
		raspberrypi
		arduino
		conversational_ai
	}
	edge [color=orange]
	Gina -- {
		node [style="filled" fontsize= 10 penwidth=0 fillcolor="#dbd8c8"]
		arduino
		python
		jamulus
	}
	edge [color=green]
	Haley -- {
		node [style="filled" fontsize= 10 penwidth=0 fillcolor="#dbd8c8"]
		folk_music
		python
		nodered
		politics
	}
	edge [color=blue]
	Ida -- {
		node [style="filled" fontsize= 10 penwidth=0 fillcolor="#dbd8c8"]
		folk_music
		banjo
	}
	edge [color=purple]
	Jennifer -- {
		node [style="filled" fontsize= 10 penwidth=0 fillcolor="#dbd8c8"]
		arduino
		politics
		banjo
		folk_music
		conversational_ai

	}
	edge [color=red]
	Kyle -- {
		node [style="filled" fontsize= 10 penwidth=0 fillcolor="#dbd8c8"]
		politics
		python
		conversational_ai
	}
	
}
```
The final product can be used to map both team members to the tasks you collaborate on, and tasks to the team members involved:

<figure>
<img src="/assets/images/contact_skeleton.png" alt="contact_skel">
<figcaption>Brian's contact-task graph</figcaption>
</figure>

## Wait a minute, how did you go from file to image?

You can generate DOT graphs online with this great website:
[dreampuf.github.io/GraphvizOnline](https://dreampuf.github.io/GraphvizOnline/#graph%20contacts_tasks%20%7B%0A%09fontname%3DArial%3B%0A%09layout%3Dtwopi%3B%20%0A%09graph%20%5Branksep%3D3%5D%20%5Boverlap%3Dtrue%5D%5Broot%3DBrian%5D%3B%0A%09edge%20%5Bpenwidth%3D1%20color%3D%22%23000000%22%5D%0A%09node%20%5Bfontname%3DBahnschrift%5D%0A%09node%20%5Bstyle%3D%22filled%22%20fontsize%3D15%20penwidth%3D0%20fillcolor%3D%22%23c96463%22%5D%0A%09Brian%20--%20%7B%0A%09%09node%20%5Bstyle%3D%22filled%22%20fontsize%3D%2010%20penwidth%3D0%20fillcolor%3D%22%23d9c762%22%5D%0A%09%09Adam%0A%09%09Brad%0A%09%09Chris%0A%09%09Donald%0A%09%09Edward%0A%09%09Frank%0A%09%09Gina%0A%09%09Haley%0A%09%09Ida%0A%09%09Jennifer%0A%09%09Kyle%0A%0A%09%7D%0A%09node%20%5Bstyle%3D%22filled%22%20fontsize%3D%2015%20penwidth%3D0%20fillcolor%3D%22%23d9c762%22%5D%0A%09edge%20%5Bcolor%3Dred%5D%0A%09Adam%20--%20%7B%0A%09%09node%20%5Bstyle%3D%22filled%22%20fontsize%3D%2010%20penwidth%3D0%20fillcolor%3D%22%23dbd8c8%22%5D%0A%09%09folk_music%0A%09%09tech%0A%09%09writing%0A%09%09linguistics%0A%09%09public_speaking%0A%09%09retro_computing%0A%09%09conversational_ai%0A%09%09jamulus%0A%09%09%09%09%0A%0A%0A%09%7D%0A%09edge%20%5Bcolor%3Dorange%5D%0A%09Brad%20--%20%7B%0A%09%09node%20%5Bstyle%3D%22filled%22%20fontsize%3D%2010%20penwidth%3D0%20fillcolor%3D%22%23dbd8c8%22%5D%0A%09%09folk_music%0A%09%09raspberrypi%0A%09%09guitar%0A%09%09jamulus%0A%09%09linguistics%0A%09%09public_speaking%0A%09%7D%0A%09edge%20%5Bcolor%3Dgreen%5D%0A%09Chris%20--%20%7B%0A%09%09node%20%5Bstyle%3D%22filled%22%20fontsize%3D%2010%20penwidth%3D0%20fillcolor%3D%22%23dbd8c8%22%5D%0A%09%09writing%0A%09%09linguistics%0A%09%7D%0A%09edge%20%5Bcolor%3Dblue%5D%0A%09Donald%20--%20%7B%0A%09%09node%20%5Bstyle%3D%22filled%22%20fontsize%3D%2010%20penwidth%3D0%20fillcolor%3D%22%23dbd8c8%22%5D%0A%09%09tech%0A%09%09python%0A%09%09nodered%0A%09%7D%0A%09edge%20%5Bcolor%3Dpurple%5D%0A%09Edward--%20%7B%0A%09%09node%20%5Bstyle%3D%22filled%22%20fontsize%3D%2010%20penwidth%3D0%20fillcolor%3D%22%23dbd8c8%22%5D%0A%09%09nodered%0A%09%09tech%0A%09%7D%0A%09edge%20%5Bcolor%3Dred%5D%0A%09Frank%20--%20%7B%0A%09%09node%20%5Bstyle%3D%22filled%22%20fontsize%3D%2010%20penwidth%3D0%20fillcolor%3D%22%23dbd8c8%22%5D%0A%09%09raspberrypi%0A%09%09arduino%0A%09%09conversational_ai%0A%09%7D%0A%09edge%20%5Bcolor%3Dorange%5D%0A%09Gina%20--%20%7B%0A%09%09node%20%5Bstyle%3D%22filled%22%20fontsize%3D%2010%20penwidth%3D0%20fillcolor%3D%22%23dbd8c8%22%5D%0A%09%09arduino%0A%09%09python%0A%09%09jamulus%0A%09%7D%0A%09edge%20%5Bcolor%3Dgreen%5D%0A%09Haley%20--%20%7B%0A%09%09node%20%5Bstyle%3D%22filled%22%20fontsize%3D%2010%20penwidth%3D0%20fillcolor%3D%22%23dbd8c8%22%5D%0A%09%09folk_music%0A%09%09python%0A%09%09nodered%0A%09%09politics%0A%09%7D%0A%09edge%20%5Bcolor%3Dblue%5D%0A%09Ida%20--%20%7B%0A%09%09node%20%5Bstyle%3D%22filled%22%20fontsize%3D%2010%20penwidth%3D0%20fillcolor%3D%22%23dbd8c8%22%5D%0A%09%09folk_music%0A%09%09banjo%0A%09%7D%0A%09edge%20%5Bcolor%3Dpurple%5D%0A%09Jennifer%20--%20%7B%0A%09%09node%20%5Bstyle%3D%22filled%22%20fontsize%3D%2010%20penwidth%3D0%20fillcolor%3D%22%23dbd8c8%22%5D%0A%09%09arduino%0A%09%09politics%0A%09%09banjo%0A%09%09folk_music%0A%09%09conversational_ai%0A%0A%09%7D%0A%09edge%20%5Bcolor%3Dred%5D%0A%09Kyle%20--%20%7B%0A%09%09node%20%5Bstyle%3D%22filled%22%20fontsize%3D%2010%20penwidth%3D0%20fillcolor%3D%22%23dbd8c8%22%5D%0A%09%09politics%0A%09%09python%0A%09%09conversational_ai%0A%09%7D%0A%09%0A%7D):

<figure>
<img src="/assets/images/graphvizonline.png" alt="graphvizdreampuf">
<figcaption>Copy and paste your file on the left and see it generated on the right.</figcaption>
</figure>

Alternatively, there is a [great extension available](https://marketplace.visualstudio.com/items?itemName=EFanZh.graphviz-preview) for the programming environment, VSCode.