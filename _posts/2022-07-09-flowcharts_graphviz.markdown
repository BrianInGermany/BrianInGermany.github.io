---
layout: post
title:  "Code Your Flow: Write the Logic, Render the Image"
description: "Create elegant flowcharts in Graphviz without worrying about layout."
date:   2022-07-09 23:15:00 +0100
tags: thinking-aids graphviz conversational-ai flow-graphing
header:
  teaser: "/assets/images/flow.png"
---
Create elegant flowcharts in Graphviz without worrying about layout.
<a href="/assets/flow.dot" download="flow.dot">
  <img src="/assets/images/flow.png" alt="flow" width="100%">
</a>

By defining flows as text, you can focus on the logic and let the rendering engine take care of the rest. Plus, you can take full advantage of version control to pinpoint changes and diffs.

The [Graphviz](https://graphviz.org) framework was [developed by AT&T Labs Research](https://en.wikipedia.org/wiki/Graphviz) as an open-source tool package for modeling and representing graphs textually.

The [DOT language](https://www.graphviz.org/doc/info/lang.html) is the reasonably intuitive markup language used to define the graphs.

## Flowcharting in Graphviz
The basic concept behind flowcharting in Graphviz is to first define your nodes, and then describe the connections they have between each other.

By separating the logical aspect of flow writing from the visual aspect, you can focus on the data and avoid the distraction of layout adjustment.

## Define nodes
The first part of creating a code-based flow is to define your nodes' shape, color and contents. Each node is declared on a new line and given a unique name.

Certain keywords, like `node`, are universal keywords, whose styling is applied to all nodes thereafter (until redefined).

The very first line of the graph denotes that the data below will form a directional graph, or `digraph`, and is necessary for the renderer to work right. The graph type is followed by a unique name.

```dot

digraph tel_flow {


// NODE DEFINITIONS
    // start nodes
    // this definition also includes graph-wide definitions for fill and font
    node[style=filled,shape=circle,color=black,fontname="Work Sans Light 300"]
        start[shape=circle,color=black]

    // end nodes
    node[shape=doublecircle,color=black]
        end[shape=doublecircle,color=black]

    // prompt nodes
    node[shape=box,color=lightblue]
        prompt_welcome[label="Willkommen
            beim Telefonkontakt der ABC-
            Krankenkasse! Ein Kundenagent 
            ist gleich für Sie da."]
        prompt_vnr[label="Bevor ich Sie verbinde,
            sagen Sie mir bitte Ihre
            Versichertennummer. Sie beginnt 
            mit einem Buchstaben, gefolgt
            von 8 Ziffern"]
        prompt_vnr_fail[label="Das hat leider nicht geklappt. 
            Probieren wirs nochmal.
            Sagen Sie mir bitte Ihre
            Versichertennummer."]
        prompt_vnr_success[label="Danke! Mit welchem Thema 
            können wir Sie heute unterstützen?"]
        prompt_anliegen_success[label="Zu Thema XX
            unterstützt Sie gleich ein Kundenagent.
            Ich verbinde Sie."]
        prompt_connect_agent[label="Ich verbinde Sie mit
            einem Kundenagenten."]  
        prompt_nicht_verstanden_anliegen[label="Ich konnte Sie leider
            nicht verstehen. Um welchen 
            Themenkomplex geht es?"]

    // utterance nodes
    node[shape=box,color=yellowgreen]
        utterance_vnr[label="VNR-Utterance"]
        utterance_anliegen[label="Anliegen-Utterance"]

    // nlu nodes
    node[shape=invhouse,color=lightgray]
        nlu_vnr[label="NLU: Versichertennr.?"]
        nlu_anliegen[label="NLU: Anliegen?"]

    // intent nodes
    node[shape=house,color=lightgray]
        intent_vnr_no_intent[label="VNR_NO_INTENT"]
        intent_vnr_agent[label="VNR_AGENT"]
        intent_vnr_vnr[label="VNR_VNR"]
        intent_anliegen_no_intent[label="ANLIEGEN_NO_INTENT"]
        intent_anliegen_agent[label="ANLIEGEN_AGENT"]
        intent_anliegen_xx[label="ANLIEGEN_XX"]
    
    // logic nodes
    node[shape=diamond,color=lightgray]  
        logic_zweitversuch_vnr[label="Zweitversuch V-Nr?"]
        logic_zweitversuch_anliegen[label="Zweitversuch Anliegen?"]
```
## Define Relationships
Next, the predefined nodes need to be connected to eath other with arrows. To make the flow clearer, subgraphs can be used to cluster nodes that belong to the same task or component. 

The `->` arrow represents the direction of the connnection between the node names before and after it. Just like with the nodes, the connections can also have labels, defineable in brackets.

The subgraphs represent the big blue boxes in the image, and can also be styled with different colors, rounding, labels, etc. These are the values followed by equals signs. Pro tip: Subgraph names must start with "cluster".

```dot

// SUBGRAPH AND CONNECTION DEFINITIONS

subgraph cluster_welcome {
    label = "Willkommen"
    color = blue
    start -> prompt_welcome

}

subgraph cluster_vnr {
    label = "Versichertennummer verstehen"
    color = blue
    prompt_welcome -> prompt_vnr
    utterance_vnr -> nlu_vnr
    nlu_vnr -> intent_vnr_agent
    nlu_vnr -> intent_vnr_vnr
    nlu_vnr -> intent_vnr_no_intent
    intent_vnr_no_intent -> logic_zweitversuch_vnr
    prompt_vnr -> utterance_vnr
    logic_zweitversuch_vnr -> prompt_vnr_fail [label="nein"]
    prompt_vnr_fail -> utterance_vnr

}
    

subgraph cluster_anliegen {
    label = "Anliegen verstehen"
    color = blue
    prompt_vnr_success -> utterance_anliegen
    utterance_anliegen -> nlu_anliegen
    nlu_anliegen -> intent_anliegen_xx
    nlu_anliegen -> intent_anliegen_agent
    nlu_anliegen -> intent_anliegen_no_intent
    intent_anliegen_no_intent -> logic_zweitversuch_anliegen
    logic_zweitversuch_anliegen -> prompt_nicht_verstanden_anliegen [label="nein"]
    prompt_nicht_verstanden_anliegen -> utterance_anliegen
    intent_vnr_vnr -> prompt_vnr_success



}
subgraph cluster_to_agent {
    label = "Übergang zum Agenten"
    color = blue
    logic_zweitversuch_vnr -> prompt_connect_agent [label="ja"]
    logic_zweitversuch_anliegen -> prompt_connect_agent [label="ja"]
    intent_vnr_agent -> prompt_connect_agent
    intent_anliegen_agent -> prompt_connect_agent
    intent_anliegen_xx -> prompt_anliegen_success
    prompt_anliegen_success -> end
    prompt_connect_agent -> end


}

}
```
Using subgraphs causes subgraphs to be layouted individually. Here is the above example as one single graph:

<a href="/assets/flow_nosubs.dot" download="flow_noubs.dot">
  <img src="/assets/images/flow_nosubs.png" alt="flow_nosubs" width="100%">
</a>

## Arterial Flow Charts
Plotting a chart of all the possible tips and turns of the flow paths is well and good. But if you're trying to make business decisions about the user journeys most central to your business goals, what information does the standard flow chart offer to support?
<img align="right" src="/assets/images/human_body.png" alt="vascular_system" width="25%">

Imagine trying to understand the human vascular system without an indication of how big each blood vessel is: you would have no idea about how much traffic is going through the various pipelines, and they all would appear equally important.

But they're not. 

So help business deciders prioritize user journeys by telling them which flow paths are the most important-- visually.

<a href="/assets/flow_arterial.dot" download="flow_arterial.dot">
  <img src="/assets/images/arterieContrast.png" alt="flow_arterial" width="100%">
</a>

Click the above image to download the example arterial flow, or just use the `edge[penwidth=1]` label above the edges you want to make thicker or thinner. 
## Rendering the Image
[VScode](https://code.visualstudio.com/), with the [Graphviz Preview](https://marketplace.visualstudio.com/items?itemName=EFanZh.graphviz-preview) extension, is a great tool for creating Graphviz graphs that allows you to render in a parallel window as you type. 

But if you want to try out Graphviz without installing anything, just go to the online Graphviz editor, [dreampuf.github.io](https://dreampuf.github.io/GraphvizOnline/#digraph%20tel_flow%20%7B%0A%20%20%20%20%2F%2F%20define%20font%20for%20subgraph%20headings%0A%20%20%20%20graph%5Bfontname%3D%22Trebuchet%20MS%22%5D%0A%2F%2F%20NODE%20DEFINITIONS%0A%20%20%20%20%2F%2F%20start%20nodes%0A%20%20%20%20%2F%2F%20this%20definition%20also%20includes%20graph-wide%20definitions%20for%20filling%20and%20font%0A%20%20%20%20node%5Bstyle%3Dfilled%2Cshape%3Dcircle%2Ccolor%3Dblack%2Cfontname%3D%22Trebuchet%20MS%22%5D%0A%20%20%20%20%20%20%20%20start%5Bshape%3Dcircle%2Ccolor%3Dblack%5D%0A%0A%20%20%20%20%2F%2F%20end%20nodes%0A%20%20%20%20node%5Bstyle%3Dfilled%2Cshape%3Ddoublecircle%2Ccolor%3Dblack%5D%0A%20%20%20%20%20%20%20%20end%5Bshape%3Ddoublecircle%2Ccolor%3Dblack%5D%0A%0A%20%20%20%20%2F%2F%20prompt%20nodes%0A%20%20%20%20node%5Bstyle%3Dfilled%2Cshape%3Dbox%2Ccolor%3Dlightblue%5D%0A%20%20%20%20%20%20%20%20prompt_welcome%5Blabel%3D%22Willkommen%0A%20%20%20%20%20%20%20%20%20%20%20%20beim%20Telefonkontakt%20der%20ABC-%0A%20%20%20%20%20%20%20%20%20%20%20%20Krankenkasse!%20Ein%20Kundenagent%20%0A%20%20%20%20%20%20%20%20%20%20%20%20ist%20gleich%20f%C3%BCr%20Sie%20da.%22%5D%0A%20%20%20%20%20%20%20%20prompt_vnr%5Blabel%3D%22Bevor%20ich%20Sie%20verbinde%2C%0A%20%20%20%20%20%20%20%20%20%20%20%20sagen%20Sie%20mir%20bitte%20Ihre%0A%20%20%20%20%20%20%20%20%20%20%20%20Versichertennummer.%20Sie%20beginnt%20%0A%20%20%20%20%20%20%20%20%20%20%20%20mit%20einem%20Buchstaben%2C%20gefolgt%0A%20%20%20%20%20%20%20%20%20%20%20%20von%208%20Ziffern%22%5D%0A%20%20%20%20%20%20%20%20prompt_vnr_fail%5Blabel%3D%22Das%20hat%20leider%20nicht%20geklappt.%20%0A%20%20%20%20%20%20%20%20%20%20%20%20Probieren%20wirs%20nochmal.%0A%20%20%20%20%20%20%20%20%20%20%20%20Sagen%20Sie%20mir%20bitte%20Ihre%0A%20%20%20%20%20%20%20%20%20%20%20%20Versichertennummer.%22%5D%0A%20%20%20%20%20%20%20%20prompt_vnr_success%5Blabel%3D%22Danke!%20Mit%20welchem%20Thema%20%0A%20%20%20%20%20%20%20%20%20%20%20%20k%C3%B6nnen%20wir%20Sie%20heute%20unterst%C3%BCtzen%3F%22%5D%0A%20%20%20%20%20%20%20%20prompt_anliegen_success%5Blabel%3D%22Zu%20Thema%20XX%0A%20%20%20%20%20%20%20%20%20%20%20%20unterst%C3%BCtzt%20Sie%20gleich%20ein%20Kundenagent.%0A%20%20%20%20%20%20%20%20%20%20%20%20Ich%20verbinde%20Sie.%22%5D%0A%20%20%20%20%20%20%20%20prompt_connect_agent%5Blabel%3D%22Ich%20verbinde%20Sie%20mit%0A%20%20%20%20%20%20%20%20%20%20%20%20einem%20Kundenagenten.%22%5D%20%20%0A%20%20%20%20%20%20%20%20prompt_nicht_verstanden_anliegen%5Blabel%3D%22Ich%20konnte%20Sie%20leider%0A%20%20%20%20%20%20%20%20%20%20%20%20nicht%20verstehen.%20Um%20welchen%20%0A%20%20%20%20%20%20%20%20%20%20%20%20Themenkomplex%20geht%20es%3F%22%5D%0A%0A%20%20%20%20%2F%2F%20utterance%20nodes%0A%20%20%20%20node%5Bstyle%3Dfilled%2Cshape%3Dbox%2Ccolor%3Dyellowgreen%5D%0A%20%20%20%20%20%20%20%20utterance_vnr%5Blabel%3D%22VNR-Utterance%22%5D%0A%20%20%20%20%20%20%20%20utterance_anliegen%5Blabel%3D%22Anliegen-Utterance%22%5D%0A%0A%20%20%20%20%2F%2F%20nlu%20nodes%0A%20%20%20%20node%5Bstyle%3Dfilled%2Cshape%3Dinvhouse%2Ccolor%3Dlightgray%5D%0A%20%20%20%20%20%20%20%20nlu_vnr%5Blabel%3D%22NLU%3A%20Versichertennr.%3F%22%5D%0A%20%20%20%20%20%20%20%20nlu_anliegen%5Blabel%3D%22NLU%3A%20Anliegen%3F%22%5D%0A%0A%20%20%20%20%2F%2F%20intent%20nodes%0A%20%20%20%20node%5Bstyle%3Dfilled%2Cshape%3Dhouse%2Ccolor%3Dlightgray%5D%0A%20%20%20%20%20%20%20%20intent_vnr_no_intent%5Blabel%3D%22VNR_NO_INTENT%22%5D%0A%20%20%20%20%20%20%20%20intent_vnr_agent%5Blabel%3D%22VNR_AGENT%22%5D%0A%20%20%20%20%20%20%20%20intent_vnr_vnr%5Blabel%3D%22VNR_VNR%22%5D%0A%20%20%20%20%20%20%20%20intent_anliegen_no_intent%5Blabel%3D%22ANLIEGEN_NO_INTENT%22%5D%0A%20%20%20%20%20%20%20%20intent_anliegen_agent%5Blabel%3D%22ANLIEGEN_AGENT%22%5D%0A%20%20%20%20%20%20%20%20intent_anliegen_xx%5Blabel%3D%22ANLIEGEN_XX%22%5D%0A%20%20%20%20%0A%20%20%20%20%2F%2F%20logic%20nodes%0A%20%20%20%20node%5Bstyle%3Dfilled%2Cshape%3Ddiamond%2Ccolor%3Dlightgray%5D%20%20%0A%20%20%20%20%20%20%20%20logic_zweitversuch_vnr%5Blabel%3D%22Zweitversuch%20V-Nr%3F%22%5D%0A%20%20%20%20%20%20%20%20logic_zweitversuch_anliegen%5Blabel%3D%22Zweitversuch%20Anliegen%3F%22%5D%0A%0A%2F%2F%20SUBGRAPH%20AND%20CONNECTION%20DEFINITIONS%0A%0Asubgraph%20cluster_welcome%20%7B%0A%20%20%20%20label%20%3D%20%22Willkommen%22%0A%20%20%20%20color%20%3D%20blue%0A%20%20%20%20edge%5Bpenwidth%3D5%5D%0A%20%20%20%20start%20-%3E%20prompt_welcome%0A%0A%7D%0A%0Asubgraph%20cluster_vnr%20%7B%0A%20%20%20%20label%20%3D%20%22Versichertennummer%20verstehen%22%0A%20%20%20%20color%20%3D%20blue%0A%20%20%20%20edge%5Bpenwidth%3D5%5D%0A%20%20%20%20prompt_welcome%20-%3E%20prompt_vnr%0A%20%20%20%20prompt_vnr%20-%3E%20utterance_vnr%0A%20%20%20%20utterance_vnr%20-%3E%20nlu_vnr%0A%20%20%20%20nlu_vnr%20-%3E%20intent_vnr_vnr%0A%20%20%20%20edge%5Bpenwidth%3D2.5%5D%0A%20%20%20%20nlu_vnr%20-%3E%20intent_vnr_agent%0A%20%20%20%20edge%5Bpenwidth%3D1%5D%0A%20%20%20%20%0A%20%20%20%20%0A%20%20%20%20%0A%20%20%20%20%0A%20%20%20%20nlu_vnr%20-%3E%20intent_vnr_no_intent%0A%20%20%20%20intent_vnr_no_intent%20-%3E%20logic_zweitversuch_vnr%0A%20%20%20%20logic_zweitversuch_vnr%20-%3E%20prompt_vnr_fail%20%5Blabel%3D%22nein%22%2Cfontname%3D%22Trebuchet%20MS%22%5D%0A%20%20%20%20prompt_vnr_fail%20-%3E%20utterance_vnr%0A%0A%7D%0A%20%20%20%20%0A%0Asubgraph%20cluster_anliegen%20%7B%0A%20%20%20%20label%20%3D%20%22Anliegen%20verstehen%22%0A%20%20%20%20color%20%3D%20blue%0A%20%20%20%20edge%5Bpenwidth%3D5%5D%0A%20%20%20%20intent_vnr_vnr%20-%3E%20prompt_vnr_success%0A%20%20%20%20prompt_vnr_success%20-%3E%20utterance_anliegen%0A%20%20%20%20utterance_anliegen%20-%3E%20nlu_anliegen%0A%20%20%20%20nlu_anliegen%20-%3E%20intent_anliegen_xx%0A%0A%0A%20%20%20%20edge%5Bpenwidth%3D2.5%5D%0A%20%20%20%20nlu_anliegen%20-%3E%20intent_anliegen_agent%0A%0A%20%20%20%20edge%5Bpenwidth%3D1%5D%0A%20%20%20%20nlu_anliegen%20-%3E%20intent_anliegen_no_intent%0A%20%20%20%20intent_anliegen_no_intent%20-%3E%20logic_zweitversuch_anliegen%0A%20%20%20%20logic_zweitversuch_anliegen%20-%3E%20prompt_nicht_verstanden_anliegen%20%5Blabel%3D%22nein%22%2Cfontname%3D%22Trebuchet%20MS%22%5D%0A%20%20%20%20prompt_nicht_verstanden_anliegen%20-%3E%20utterance_anliegen%0A%20%20%20%20%0A%0A%0A%0A%7D%0Asubgraph%20cluster_to_agent%20%7B%0A%20%20%20%20label%20%3D%20%22%C3%9Cbergang%20zum%20Agenten%22%0A%20%20%20%20color%20%3D%20blue%0A%20%20%20%20edge%5Bpenwidth%3D5%5D%0A%20%20%20%20intent_anliegen_xx%20-%3E%20prompt_anliegen_success%0A%20%20%20%20prompt_anliegen_success%20-%3E%20end%0A%20%20%20%20edge%5Bpenwidth%3D2.5%5D%0A%20%20%20%20intent_anliegen_agent%20-%3E%20prompt_connect_agent%0A%20%20%20%20intent_vnr_agent%20-%3E%20prompt_connect_agent%0A%20%20%20%20prompt_connect_agent%20-%3E%20end%0A%20%20%20%20edge%5Bpenwidth%3D1%5D%0A%20%20%20%20logic_zweitversuch_vnr%20-%3E%20prompt_connect_agent%20%5Blabel%3D%22ja%22%2Cfontname%3D%22Trebuchet%20MS%22%5D%0A%20%20%20%20logic_zweitversuch_anliegen%20-%3E%20prompt_connect_agent%20%5Blabel%3D%22ja%22%2Cfontname%3D%22Trebuchet%20MS%22%5D%0A%0A%0A%7D%0A%0A%7D%0A%0A%0A%0A%0A%0A%0A).

If you want to go the VScode route, youll first need to install [graphviz](https://graphviz.org/download/) on your system.

Then, all you need to do is create your graph file with a `.dot` ending in VScode and then run the command `Graphviz: Open Preview to the Side`  using `CTRL/CMD-SHIFT-P`.

![](/assets/images/graphviz_preview.png)

From this screen, you can export to the file format of your choice.

## Develop Collaboratively and Easily Inspect Diffs
In VScode, you can use git to track versions of your graph as you develop and change it. Additionally, you can use the compare diff functionality to see exactly what part of the graph was changed in each version.

![](/assets/images/diff_flow.png)

## Conclusion
Creating flowcharts from code is a great way to focus your thoughts on the raw flow structure itself. But it also takes the visual tidying work off your shoulders, and makes collaboration easier by enabling line-for-line comparability of versions.