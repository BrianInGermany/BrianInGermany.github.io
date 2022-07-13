---
layout: post
title:  "Crossfunctional Conversational AI Flows with Nodered"
description: "Design CAI user journeys with code snippets, external queries and audio playback."
date:   2022-07-13 21:15:00 +0100
tags: nodered conversational-ai thinking-aids
header:
  teaser: "/assets/images/noderedShot.png"
---

Design CAI user journeys with code snippets, external queries and audio playback.
<video src="/assets/images/noderedCAIflow.mp4" autoplay loop controls width="100%"></video>

## CAI on Nodered?
There are several packages for Nodered out there for building bots with CAI products, such as IBM Watson, Amazon Lex or the Telegram chatbot interface.

But why is no one using Nodered for Conversational AI *design*? 
Its rich visual UI and powerful low-code features allow for a crossfunctional design experience.

- Utilize local browser TTS to "speak through" prompts and utterances
  - With different voices for the full computer-acted experience
- Utilize code snippets to pre-sketch logic components for developers
- Include http calls and responses
  - To query live NLU models within your design
  - To query information/text services
  - Other external services relevant to design
- Export flow to a machine-readable graph JSON 
  - JSON can be postprocessed to calculate and list all possible flow paths
  - Statistics on longest and shortest path combinations
  
<video src="/assets/images/noderedNodes.mp4" autoplay loop controls width="100%"></video>
