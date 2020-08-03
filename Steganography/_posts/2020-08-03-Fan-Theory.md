---
layout: post
title: "Fan Theory"
author: "INXS_JOY"
tags: ['Steganography']
---



When secrets are hidden, fans can up with the wonkiest theories.

```
I:54:61
I:33:74
I:18:74
I:74:44
I:4:53


I:14:45
I:23:61
I:63:63
I:75:19
I:13:56

I:20:6
I:56:6
I:2:60
I:12:45
I:52:78
I:1:7

I:18:73
I:19:16
I:16:55
I:75:65
I:42:78
I:12:85

I:6:7
I:53:38
I:38:37
I:60:50
I:13:42
```

* [theory.txt](https://ctf.hacktivitycon.com/files/b7bcbcaec5caef0faa4647e971026ed3/theory.txt?token=eyJ1c2VyX2lkIjoxMzQ0LCJ0ZWFtX2lkIjpudWxsLCJmaWxlX2lkIjoxMTN9.XyfYOw.NCtNbJ4WIMfgjkdknvZOinUZUDQ)

## Solution

* Treating the txt file as a 2D matrix where row represents line number and column representing the nth character of the line, we wrote this script to extract the characters:

```python
f = open("asciif.txt","rb").read()

st = '''I:54:61
I:33:74
I:18:74
I:74:44
I:4:53
I:14:45
I:23:61
I:63:63
I:75:19
I:13:56
I:20:6
I:56:6
I:2:60
I:12:45
I:52:78
I:1:7
I:18:73
I:19:16
I:16:55
I:75:65
I:42:78
I:12:85
I:6:7
I:53:38
I:38:37
I:60:50
I:13:42'''.split('\n')

for i in st:
    if len(i) == 0:
        print()
        continue
    ind = i.split(':')
    st = int(ind[1])
    strt = f.index((str(st) + '.').encode())
    print(chr(f[strt + int(ind[2]) - 1]),end='')
```

* We end up with this text after running the python code, `eluw{eei jyluduwqjylusetui}`. 
* Now, let's try to gather character from the (right position-1) i.e the characters preceeding the characters we just got. We end up with the following `vbqo{fply hAhi oenelsnvep }`. 
* Now I noticed that upon decoding `vbqo{fply hAhi oenelsnvep }` by caesar 16, we get the first three letters as `fla` and rest all gibberish. 
*  I thought why not see what happens when we caesar 16 decode the first text we got `eluw{eei jyluduwqjylusetui}`. Which resulted in this `oveg{oos tivenegativecodes}`. At this point you can just guess the flag.
## Flag
```
flag{positivenegativecodes}
```
