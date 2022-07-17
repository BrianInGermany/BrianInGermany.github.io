---
layout: post
title:  "Crossfunctional CAI Design with Node-Red"
description: "Design conversational user journeys with code snippets, external queries and audio playback."
date:   2022-07-11 21:30:00 +0100
tags: nodered conversational-ai flow-graphing
header:
  teaser: "/assets/images/noderedShot.png"
---
Design CAI user journeys with code snippets, external queries and audio playback.
<video src="/assets/images/noderedCAIflow.mp4" controls width="100%"></video>
        
## CAI on Nodered?
There are several packages for [Nodered](https://nodered.org/) out there for building bots with CAI products, such as IBM Watson, Amazon Lex or the Telegram chatbot interface.

But why is no one using Nodered for Conversational AI *design*? 
Its rich visual UI and powerful low-code features allow for a crossfunctional design experience.

- Utilize local browser TTS to "speak through" prompts and utterances
  - Path by path
- Utilize code snippets to pre-sketch logic components for developers
- Store complex or repeated processes in [subflows](https://nodered.org/docs/user-guide/editor/workspace/subflows)
- Include http calls and responses
  - To query live NLU models within your design
  - To query information/text services
  - Other external services relevant to design
- Export flow to a machine-readable graph JSON 
  - JSON can be postprocessed to calculate and list all possible flow paths
  - Statistics on longest and shortest path combinations

### [Download this flow](/assets/ABCflow.json)