---
layout: post
title:  "Code Your Flow: Write the Logic, Render the Image"
description: "Create elegant flowcharts in Graphviz without worrying about layout."
date:   2022-07-09 23:15:00 +0100
tags: thinking-aids graphviz
header:
  teaser: "/assets/images/flow.png"
---
<a href="/assets/flow.pdf" download="flow">
  <img src="/assets/images/flow.png" alt="flow" width="100%">
</a>

By defining flows as text, you can focus on the logic and let the rendering engine take care of the rest. Plus, you can take full advantage of version control to pinpoint changes and diffs.

The [Graphviz](https://graphviz.org) framework was [developed by AT&T Labs Research](https://en.wikipedia.org/wiki/Graphviz) as an open-source tool package for modeling and representing graphs textually.

The [DOT language](https://www.graphviz.org/doc/info/lang.html) is the reasonably intuitive markup language used to define the graphs.

## Flowcharting in Graphviz
The basic concept behind flowcharting in Graphviz is to first define your nodes, and then describe the connections they have between each other.

By separating the logical aspect of flow writing from the visual aspect, you can focus on the data and avoid the distraction of layout adjustment.

## Define nodes
The first part of creating a code-based flow is to define your nodes' shape, color and contents. Each node is declared on a new line and given a unique name, styling and text label (in the brackets after the name).

Certain keywords, like `node`, are universal keywords, whose styling is applied to all future nodes thereafter.

The rest of the lines represent nodes themselves, for example `prompt_welcome`, which in brackets is assigned the shape `box`, color `lightblue` and a multi-line text label.

The very first line of the graph denotes that the data below will form a directional graph, or `digraph`, and is necessary for the renderer to work right. The graph type is followed by a unique name (`tel_flow`).

```dot
digraph tel_flow {
    node[style=filled]
    start[shape=circle,color=black]
    end[shape=doublecircle,color=black]
    prompt_welcome[shape=box,color=lightblue,label="Willkommen
        beim Telefonkontakt der ABC-
        Krankenkasse! Ein Kundenagent 
        ist gleich für Sie da."]
    prompt_vnr[shape=box,color=lightblue,label="Bevor ich Sie verbinde,
        sagen Sie mir bitte Ihre
        Versichertennummer. Sie beginnt 
        mit einem Buchstaben, gefolgt
        von 8 Ziffern"]
    utterance_vnr[shape=box,color=yellowgreen,label="VNR-Utterance"]
    nlu_vnr[shape=invhouse,label="NLU: Versichertennr.?"]
    nlu_anliegen[shape=invhouse,label="NLU: Anliegen?"]
    prompt_vnr_fail[shape=box,color=lightblue,label="Das hat leider nicht geklappt. 
        Probieren wirs nochmal.
        Sagen Sie mir bitte Ihre
        Versichertennummer."]
    prompt_vnr_success[shape=box,color=lightblue,label="Danke! Mit welchem Thema 
        können wir Sie heute unterstützen?"]
    utterance_anliegen[shape=box,color=yellowgreen,label="Anliegen-Utterance"]
    prompt_anliegen_success[shape=box,color=lightblue,label="Zu Thema XX
        unterstützt Sie gleich ein Kundenagent.
        Ich verbinde Sie."]
    intent_vnr_no_intent[shape=house,label="VNR_NO_INTENT"]
    intent_vnr_agent[shape=house,label="VNR_AGENT"]
    intent_vnr_vnr[shape=house,label="VNR_VNR"]
    intent_anliegen_no_intent[shape=house,label="ANLIEGEN_NO_INTENT"]
    intent_anliegen_agent[shape=house,label="ANLIEGEN_AGENT"]
    intent_anliegen_xx[shape=house,label="ANLIEGEN_XX"]
    prompt_connect_agent[shape=box,color=lightblue,label="Ich verbinde Sie mit
        einem Kundenagenten."]
    logic_zweitversuch_vnr[shape=diamond,label="Zweitversuch V-Nr?"]
    prompt_nicht_verstanden_anliegen[shape=box,color=lightblue,label="Ich konnte Sie leider
        nicht verstehen. Um welchen 
        Themenkomplex geht es?"]
    logic_zweitversuch_anliegen[shape=diamond,label="Zweitversuch Anliegen?"]

```
## Define Relationships
Next, the predefined nodes need to be connected to eath other with arrows. To make the flow clearer, subgraphs can be used to cluster nodes that belong to the same task or component. 

The `->` arrow represents the direction of the connnection between the node names before and after it. Just like with the nodes, the connections can also have labels, defineable in brackets.

The subgraphs represent the big blue boxes in the image, and can also be styled with different colors, rounding,labels, etc. These are the values followed by equals signs. Subgraphs start and end with curly braces.

```dot

subgraph cluster_welcome {
    label = "Willkommen"
    color = blue
    start -> prompt_welcome

}

subgraph cluster_vnr {
    label = "Versichertennummer verstehen"
    color = blue
    prompt_welcome -> prompt_vnr
    prompt_vnr -> utterance_vnr
    utterance_vnr -> nlu_vnr
    nlu_vnr -> intent_vnr_agent
    nlu_vnr -> intent_vnr_vnr
    nlu_vnr -> intent_vnr_no_intent
    intent_vnr_no_intent -> logic_zweitversuch_vnr
    logic_zweitversuch_vnr -> prompt_vnr_fail [label="nein"]
}
    logic_zweitversuch_vnr -> prompt_connect_agent [label="ja"]
    prompt_connect_agent -> end
    prompt_vnr_fail -> utterance_vnr
    prompt_vnr_success -> utterance_anliegen
    utterance_anliegen -> nlu_anliegen

subgraph cluster_anliegen {
    label = "Anliegen verstehen"
    color = blue
    intent_vnr_vnr -> prompt_vnr_success

    nlu_anliegen -> intent_anliegen_xx
    nlu_anliegen -> intent_anliegen_agent
    nlu_anliegen -> intent_anliegen_no_intent
    intent_anliegen_no_intent -> logic_zweitversuch_anliegen
    logic_zweitversuch_anliegen -> prompt_nicht_verstanden_anliegen [label="nein"]
    prompt_nicht_verstanden_anliegen -> utterance_anliegen


}
subgraph cluster_to_agent {
    label = "Übergang zum Agenten"
    color = blue
    intent_anliegen_agent -> prompt_connect_agent
    intent_vnr_agent -> prompt_connect_agent
    intent_anliegen_xx -> prompt_anliegen_success
    logic_zweitversuch_anliegen -> prompt_connect_agent [label="ja"]
    prompt_anliegen_success -> end

}

}
```

## Rendering the Image
[VScode](https://code.visualstudio.com/), with the [Graphviz Preview](https://marketplace.visualstudio.com/items?itemName=EFanZh.graphviz-preview) extension, is a great tool for creating Graphviz graphs that allows you to render in a parallel window as you type.

All you need to do is create your graph file with a `.dot` ending in VScode and then run the command `Graphviz: Open Preview to the Side`  using `CTRL/CMD-SHIFT-P`.

![](/assets/images/graphviz_preview.png)

From this screen, you can export to the file format of your choice.

## Develop Collaboratively and Easily Inspect Diffs
In VScode, you can use git to track versions of your graph as you develop and change it. Additionally, you can use the compare diff functionality to see exactly what part of the graph was changed in each version.

![](/assets/images/diff_flow.png)

## Conclusion
Creating flowcharts from code is a great way to focus your thoughts on the raw flow structure itself. But it also takes the visual tidying work off your shoulders, and makes collaboration easier by enabling line-for-line comparability across versions.