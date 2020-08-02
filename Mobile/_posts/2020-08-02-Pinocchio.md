---
layout: post
title: "Pinocchio"
author: "shreyas-sriram"
tags: ['Mobile']
---

Pinocchio just made a new app! He says it is very secure... but I think I see his nose growing...

Download the file below.<br/>
[App-release.apk](https://ctf.hacktivitycon.com/files/6fc724467e3c8680c6e1ab0942d8550e/app-release.apk?token=eyJ1c2VyX2lkIjoxMzQ0LCJ0ZWFtX2lkIjpudWxsLCJmaWxlX2lkIjoxMjl9.Xybuyg.Yf7hpahJ0fNvwdOhE9LEEaUU9_Q)

## Solution
* Download and install the apk
* Find a page which expects a 4-digit PIN
* Enter a random 4-digit PIN to understand the functionality of the application
* We see different responses depending on whether the WiFi is turned on or switched off
* This tells us that the entered PIN is being checked with an external server (can be verified using Burp Suite too)
* Since the PIN is of length 4, it is possible to brute-force the combinations
* [Configure the Android Device to work with Burp Suite](https://portswigger.net/support/configuring-an-android-device-to-work-with-burp)
* Capture the request in Burp Suite and send to Burp Intruder
	* Set payloads from `0000 - 9999`
* Find that payload `6402` returns the flag

## Flag
```
flag{lied_about_this_being_secure}
```