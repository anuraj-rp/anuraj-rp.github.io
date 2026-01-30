---
title: "Discord Stream Kit Overlay setup for Yak Collective"
date: 2023-03-14
author_profile: true
classes: wide
categories:
  - video-editing
tags:
  - video
---

I have been experimenting with livestreams over the last few months with OBS. Last weekend my friend Nathan and I set up stream kit for our [Yak Collective][YC website] study group. With some neat CSS tricks by Nathan we were able to setup discord steamkit overlay for a nice looking streaming scene. Here is what yesterday's stream looked like. 
<br/>
<iframe width="560" height="315" src="https://www.youtube.com/embed/qM_ZiKiBaLI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
<br/>

The audio still needs some work. But overall I am happy with the scene layout. The CSS added to the discord streamkit chat overlay below

```css
body { background-color: rgba(0, 0, 0, 0); margin: 0px auto; overflow: hidden;} 
div[class^='Chat_chatContainer__'] { height: 950px !important; width: auto !important; } 
div[class^='Chat_channelName__'] { float: left; width 100%; } 
ul[class^='Chat_messages__'] { height: calc(950px - 52px) !important; width: calc(100% - 16px); } 
li[class^='Chat_message__'] { max-height: none !important; }
```

The CSS extends the chat window to the entire scene instead of a small rectangular box in previous distributed systems study group videos. Next step is to update the voice channel overlay CSS and enhance the audio somehow.

[YC website]: https://www.yakcollective.org/about.html