---
layout: post
title: "Whale Watching"
author: "vishalananth"
tags: ['OSINT']
---

Where is the flag? It is not down on any map; true places never are.

Hunt down:
johnhammond/whale_watching

## Solution

The challenge name and the search string format hinted at a docker container. So I went to [Docker Hub](https://hub.docker.com/) and searched for `johnhammond/whale_watching`. We got the container!!, going into tags and clicking on latest, we get the history of the container which contains the flag.

## Flag

```
flag{call_me_ishmael}
```

