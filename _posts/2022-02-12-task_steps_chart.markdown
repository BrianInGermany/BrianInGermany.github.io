---
layout: post
title:  "Process-Graph Your Tasks"
description: "Communicate task structures to your team visually"
date:   2022-02-12 08:43:00 +0100
categories: jekyll update
tags: thinking-aids graphviz
header:
  teaser: "/assets/images/task_steps.png"
---

<img src="/assets/images/task_steps.png" alt="task_step">

If you want to model the task structure of a given project, it can make sense to list all the different tasks and subtasks, all the recurring processes that project consists of. But how can you best communicate the details of your task network?

## The Task-Process Graph

For a data structure that can represent interconnected tasks and steps, we need a collection of lists and connecting arrows:

In the above task-process graph, specific cells, or task steps, of the task nodes are connected in a flow to show what substeps pertain to which tasks, and which substeps are shared by which tasks in a many-to-one relationship.

## Drawing Tools

You can generate this data structure using DOT graphs and the `record` node style.
For example online, with this great website (code to the sample chart included):
[dreampuf.github.io/GraphvizOnline](https://dreampuf.github.io/GraphvizOnline/#digraph%20tasks_steps%20%7B%0Agraph%20%5B%0A%20%20%20%20labelloc%3D%22t%22%0A%20%20%20%20fontsize%3D30%0A%20%20%20%20label%3D%22Task%20Chart%3A%20Making%20a%20Github%20Pages%20Website%22%0A%20%20%20%20rankdir%20%3D%20%22LR%22%0A%5D%3B%0Anode%20%5B%0Afontsize%20%3D%20%2216%22%20%0A%5D%3B%0Aedge%20%5B%0A%5D%3B%0A%22CREATE%20A%20GITHUB%20PAGES%20WEBSITE%22%20%5B%0Alabel%20%3D%20%22%3Cf0%3E%20CREATE%20GITHUB%20PAGES%20WEBSITE%20%7C%20%3Cf1%3E%201.%20create%20a%20github%20repository%20%7C%20%3Cf2%3E%202.%20buy%20domain%20on%20namecheap%20%7C%0A%3Cf3%3E%203.%20link%20github%20pages%20to%20domain%22%0Ashape%20%3D%20%22record%22%0A%5D%3B%0A%22CREATE%20A%20GITHUB%20REPOSITORY%22%20%5B%0Alabel%20%3D%20%22%3Cf0%3E%20CREATE%20A%20GITHUB%20REPOSITORY%20%7C%20%3Cf1%3E%201.%20create%20a%20github%20account%20%7C%20%3Cf2%3E%202.%20press%20button%20for%20new%20repository%20%7C%20%3Cf3%3E%203.%20create%20local%20repository%20and%20push%22%0Ashape%20%3D%20%22record%22%0A%5D%3B%0A%22LINK%20GITHUB%20PAGES%20TO%20DOMAIN%22%20%5B%0Alabel%20%3D%20%22%3Cf0%3E%20LINK%20GITHUB%20PAGES%20TO%20DOMAIN%20%7C%20%3Cf1%3E%201.%20configure%20domain%20records%20on%20namecheap%20%7C%20%3Cf2%3E%202.%20enter%20domain%20name%20on%20github%20pages%22%0Ashape%20%3D%20%22record%22%0A%5D%3B%0A%0A%22CREATE%20LOCAL%20REPOSITORY%20AND%20PUSH%22%20%5B%0Alabel%20%3D%20%22%3Cf0%3E%20CREATE%20LOCAL%20REPOSITORY%20AND%20PUSH%20%7C%20%3Cf1%3E%201.%20go%20to%20command%20line%20in%20desired%20directory%20%7C%20%3Cf2%3E%202.%20create%20repo%20with%20%60git%20init'%20%7C%20%3Cf3%3E%203.%20add%20readme%20file%20%7C%0A%20%3Cf4%3E%204.%20stage%20changes%20with%20%60git%20add%20.%60%20%7C%20%3Cf5%3E%205.%20commit%20initial%20status%20with%20%60git%20commit%20-m%20'initial%20status'%20%7C%20%3Cf6%3E%206.%20link%20repo%20to%20remote%20with%20%60git%20remote%20add%20origin%60%20%0A%20%7C%20%3Cf7%3E%207.%20push%20to%20remote%20with%20%60git%20push%20-u%20origin%20master%60%22%0Ashape%20%3D%20%22record%22%0A%5D%3B%0A%22CONFIGURE%20DOMAIN%20RECORDS%20ON%20NAMECHEAP%22%20%5B%0Alabel%20%3D%20%22%3Cf0%3E%20CONFIGURE%20DOMAIN%20RECORDS%20ON%20NAMECHEAP%20%7C%20%3Cf1%3E%201.%20login%20to%20namecheap%20dashboard%20%7C%20%3Cf2%3E%202.%20google%20the%20github%20pages%20domain%20settings%20%7C%0A%3Cf3%3E%203.%20add%20records%20to%20DNS%20as%20specified%20%7C%20%3Cf4%3E%204.%20wait%2030%20minutes%22%0Ashape%20%3D%20%22record%22%0A%5D%3B%0A%22ENTER%20DOMAIN%20NAME%20ON%20GITHUB%20PAGES%22%20%5B%0Alabel%20%3D%20%22%3Cf0%3E%20ENTER%20DOMAIN%20NAME%20ON%20GITHUB%20PAGES%20%7C%20%3Cf1%3E%201.%20go%20to%20settings%20of%20github%20repo%20%7C%20%3Cf2%3E%202.%20enter%20domain%20name%20and%20ending%20in%20github%20pages%20tab%20%7C%0A%3Cf3%3E%203.%20check%20box%20for%20'require%20https'%20%7C%20%3Cf4%3E%204.%20save%20changes%22%0Ashape%20%3D%20%22record%22%0A%5D%3B%0A%0A%22CREATE%20A%20GITHUB%20PAGES%20WEBSITE%22%3Af1%20-%3E%20%22CREATE%20A%20GITHUB%20REPOSITORY%22%3Af0%20%5B%0Aid%20%3D%200%0A%5D%3B%0A%0A%22CREATE%20A%20GITHUB%20PAGES%20WEBSITE%22%3Af3%20-%3E%20%22LINK%20GITHUB%20PAGES%20TO%20DOMAIN%22%3Af0%20%5B%0Aid%20%3D%200%0A%5D%3B%0A%22CREATE%20A%20GITHUB%20REPOSITORY%22%3Af3%20-%3E%20%22CREATE%20LOCAL%20REPOSITORY%20AND%20PUSH%22%3Af0%20%5B%0Aid%20%3D%200%0A%5D%3B%0A%22LINK%20GITHUB%20PAGES%20TO%20DOMAIN%22%3Af1%20-%3E%20%22CONFIGURE%20DOMAIN%20RECORDS%20ON%20NAMECHEAP%22%3Af0%20%5B%0Aid%20%3D%200%0A%5D%3B%0A%22LINK%20GITHUB%20PAGES%20TO%20DOMAIN%22%3Af2%20-%3E%20%22ENTER%20DOMAIN%20NAME%20ON%20GITHUB%20PAGES%22%3Af0%20%5B%0Aid%20%3D%200%0A%5D%3B%0A%0A%0A%0A%7D). Alternatively, there is a [Graphviz extension available](https://marketplace.visualstudio.com/items?itemName=EFanZh.graphviz-preview) for the programming environment, VSCode.

Another option could be to draw and connect the nodes from scratch with the amazing diagramming tool, [draw.io](https://app.diagrams.net/).

And don't forget pen and paper :grin: