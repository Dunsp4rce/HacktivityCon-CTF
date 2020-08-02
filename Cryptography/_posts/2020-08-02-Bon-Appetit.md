---
layout: post
title: "Bon Appetit"
author: "vishalananth"
tags: ['Cryptography']
---

Wow, look at the size of that! There is just so much to eat!

## Solution

We are given a file which contains the RSA parameters n,e and c. Looking at the value for n and e, we see that they are both enormous and hence the only way to break the cipher is when d is very small when compared to n. So we immediately tried Wiener attack which sadly did not work. Searching more led us to `Boneh-Durfee attack` which was more advanced than Wiener attack and works when d < n^0.292. So we tried using this script which was available at [https://github.com/mimoo/RSA-and-LLL-attacks/blob/master/boneh_durfee.sage](https://github.com/mimoo/RSA-and-LLL-attacks/blob/master/boneh_durfee.sage). After tweaking the values of delta and m for sometime we ended up with the right values `delta = 0.27 and m = 5`. This gave us the following output:

```
sage bonneh_dufree.sage 
=== checking values ===
* delta: 0.270000000000000
* delta < 0.292 True
* size of e: 1021
* size of N: 1022
* m: 5 , t: 2
=== running algorithm ===
* removing unhelpful vector 25
* removing unhelpful vector 21
* removing unhelpful vectors 1 and 2
* removing unhelpful vector 0
10 / 22  vectors are not helpful
We do not have det < bound. Solutions might not be found.
Try with highers m and t.
size det(L) - size e^(m*n) =  84
00 X 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 ~
01 X X 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 ~
02 X X X 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 
03 0 0 0 X 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 ~
04 0 0 0 X X 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 ~
05 0 0 0 X X X 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 
06 0 0 0 X X X X 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 
07 0 0 0 0 0 0 0 X 0 0 0 0 0 0 0 0 0 0 0 0 0 0 ~
08 0 0 0 0 0 0 0 X X 0 0 0 0 0 0 0 0 0 0 0 0 0 ~
09 0 0 0 0 0 0 0 X X X 0 0 0 0 0 0 0 0 0 0 0 0 ~
10 0 0 0 0 0 0 0 X X X X 0 0 0 0 0 0 0 0 0 0 0 
11 0 0 0 0 0 0 0 X X X X X 0 0 0 0 0 0 0 0 0 0 
12 0 0 0 0 0 0 0 0 0 0 0 0 X 0 0 0 0 0 0 0 0 0 ~
13 0 0 0 0 0 0 0 0 0 0 0 0 X X 0 0 0 0 0 0 0 0 ~
14 0 0 0 0 0 0 0 0 0 0 0 0 X X X 0 0 0 0 0 0 0 ~
15 0 0 0 0 0 0 0 0 0 0 0 0 X X X X 0 0 0 0 0 0 
16 0 0 0 0 0 0 0 0 0 0 0 0 X X X X X 0 0 0 0 0 
17 0 0 0 0 0 0 0 0 0 0 0 0 X X X X X X 0 0 0 0 
18 X X X 0 X X X 0 0 0 0 0 0 0 0 0 0 0 X 0 0 0 
19 0 0 0 X X X X 0 X X X X 0 0 0 0 0 0 0 X 0 0 
20 0 0 0 0 0 0 0 X X X X X 0 X X X X X 0 0 X 0 
21 0 0 0 X X X X 0 X X X X 0 0 X X X X 0 X X X 
optimizing basis of the lattice via LLL, this can take a long time
LLL is done!
looking for independent vectors in the lattice
found them, using vectors 0 and 1
=== solution found ===
private key found: 5448511435693918250863484721514292687178096328572373396537572878464059764348289027
=== 1.309525489807129 seconds ===
```

Decoding the cipher text using the private key with a python script:

```python
n = 86431753033855985150102208955150746586984567379198773779001331665367046453352820308880271669822455250275431988006538670370772552305524017849991185913742092236107854495476674896994207609393292792117921602704960758666683584350417558805524933062668049116636465650763347823718120563639928978056322149710777096619
c = 6017385445033775122298094219645257172271491520435372858165807340335108272067850311951631832540055908237902072239439990174700038153658826905580623598761388867106266417340542206012950531616502674237610428277052393911078615817819668756516229271606749753721145798023983027473008670407713937202613809743778378902
d = 5448511435693918250863484721514292687178096328572373396537572878464059764348289027
dec = pow(c,d,n)
print(bytes.fromhex(hex(dec)[2:]))
```

we get the flag.

## Flag

```
flag{bon_appetit_that_was_one_big_meal}
```
