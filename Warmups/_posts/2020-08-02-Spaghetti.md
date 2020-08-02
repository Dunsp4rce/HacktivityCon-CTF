---
layout: post
title: "Spaghetti"
author: "vishalananth"
tags: ['Warmups']
---

It's a classic, it's everyones favorite, it's spaghetti! The long noodles are the best!

## Solution

After nearly spending two days and trying everything, we come across this link: [https://www.sans.org/blog/strings-strings-are-wonderful-things/](https://www.sans.org/blog/strings-strings-are-wonderful-things/) which was the saviour and gave us the command we needed:

```
strings -el spaghetti.png
```

This command makes the unicode characters visible by taking 16-bit characters and gives us the flag.

## Flag

```
flag{wow_that_was_a_long_string_of_spaghetti}
```

