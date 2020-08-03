---
layout: post
title: "Oppossable Thumbs"
author: "INXS_JOY"
tags: ['Forensics']
---

The flag is right between your finger tips.

Download the file below.

* [thumbcache_256.db](https://ctf.hacktivitycon.com/files/95a28b7295733ca54494b2f0ccc2e620/thumbcache_256.db?token=eyJ1c2VyX2lkIjoxMzQ0LCJ0ZWFtX2lkIjpudWxsLCJmaWxlX2lkIjoxMzd9.Xyfjbg.tf1jL0xS1WdQXW8NLSotr1HJtYY)

## Solution

* We are given a thumb cache file, therefore I installed this [thumbcache viewer](https://thumbcacheviewer.github.io/). Yes, it's a Windows tool :( 

* Opening .db file on the tool we see that it has a lot of entries. Among those, one .png file had the flag.

![alt-text]({{site.baseurl}}/assets/Oppossable-Thumbs/thumbcache.png)



## Flag
```
flag{human_after_all}
```
