---
layout: post
title: "Unsubscribe"
author: "vishalananth"
tags: ['Steganography']
---

Did you know that the 'Nigerian prince' email spam still brings in over $700,000 USD per year? It's one of the most successful scams campaigns to date.

## Solution

We are given a text file which contained a usual scam email like message. I tried common stuff like viewing the hexdump, trying whitespace steganography tools like stegsnow etc.., but nothing worked. So I searched "text file steganography" and came across the link [Steganography to hide text within text](https://security.stackexchange.com/questions/20414/steganography-to-hide-text-within-text). There was a link to [https://www.spammimic.com/](https://www.spammimic.com/) in the answer. Decoding the message using spammimic, we get the flag.

## Flag

```
flag{hidden_message_in_spam}
```
