---
layout: post
title: "Mobile One"
author: "vishalananth"
tags: ['Mobile']
---

The one true mobile app.

## Solution

We download the given APK file and unzip it using:

```
unzip mobile_one.apk
```

We get all the standard files, trying out:

```
strings * | grep "flag"
```

gave us the flag.

## Flag

```
flag{strings_grep_and_more_strings}
```

