---
layout: post
title: "Private Investigator"
author: "INXS_JOY"
tags: ['Warmups']
---

We have hired you to help investigate this private key. Please use it to connect to the server like so:

ssh -i id_rsa user@jh2i.com -p 50004

## Solution

* Reading the private key file, I noticed that the file was missing a \n at the end of the file.

```
root@kali:~/Downloads# cat id_rsa 
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAABlwAAAAdzc2gtcn
NhAAAAAwEAAQAAAYEAsLiZbT/+tg8qtA3BensRcqBTP+cqchTkDR40FKpuD5e+TqzyLIYZ
II6MiU7icNw9Nb01vNQvrYxc4E/HxT8rAUBX5Yj0kqk+2V70jH2JK7dpPKJq8XLyZUUMSc
0SNjaAHNWSmvDHGCw+w0PGUqCPz9XcGZPiurmT5i54ZMPgXrAOeeX4yhyQoVos4ELm4HYS
0z0f78UIZNuaI7D9xaUGT9fy7eF256Exj+oJdvX4VNvckiurGMyOIynhysP+8iquXEOU5r
FVaGbn0C4exprRDp5He/E3DYEF64KV0VYPhmxWF/kmMB+2R3WSufT41fCcqItYuA0UWSHY
9JtCA2HrWh8by/tuGmacaDThoEhckG/cOuOGaywPeLcDQk4On3NxJH2bnCvzJrv2Nah1Dc
HFDAzn5IL8APupvYNwBId+rBAOl6+61KfLnQiryiIjwzE7/X5vsZFaa21zdZiE02LQ2K78
s3RqG2b/8+j2B+nPbcZSjW3muiyYmC4NN+LLGEOdAAAFgPKq7U7yqu1OAAAAB3NzaC1yc2
EAAAGBALC4mW0//rYPKrQNwXp7EXKgUz/nKnIU5A0eNBSqbg+Xvk6s8iyGGSCOjIlO4nDc
PTW9NbzUL62MXOBPx8U/KwFAV+WI9JKpPtle9Ix9iSu3aTyiavFy8mVFDEnNEjY2gBzVkp
rwxxgsPsNDxlKgj8/V3BmT4rq5k+YueGTD4F6wDnnl+MockKFaLOBC5uB2EtM9H+/FCGTb
miOw/cWlBk/X8u3hduehMY/qCXb1+FTb3JIrqxjMjiMp4crD/vIqrlxDlOaxVWhm59AuHs
aa0Q6eR3vxNw2BBeuCldFWD4ZsVhf5JjAftkd1krn0+NXwnKiLWLgNFFkh2PSbQgNh61of
G8v7bhpmnGg04aBIXJBv3DrjhmssD3i3A0JODp9zcSR9m5wr8ya79jWodQ3BxQwM5+SC/A
D7qb2DcASHfqwQDpevutSny50Iq8oiI8MxO/1+b7GRWmttc3WYhNNi0Niu/LN0ahtm//Po
9gfpz23GUo1t5rosmJguDTfiyxhDnQAAAAMBAAEAAAGBAKM1eY0qYyTlEP1FDwD9E/oXE4
ubBNpjbNKoqFTFqewAqqOime6A0kf9HtHY5sxwup8c5bpFBNt1HHmVdNw4IJGBSSwVtjqU
0BSU26m8bqjPNQPoxHfFPxREFrs6B63F27/FhyZNZLJwem5/83NwEiFSU3nT2Lu2lF8rX8
lAFcGdO2FdAM44X2KFE5jycKOwqGYqt4oLIFt1bP+1gEm+xPuMZzFG3zfA6TMOZDtXo0dL
3oOojNXUZRkYnw1SwewJeYCPxoEE932EccR6KLZD227L6a+SYgnnOkr2yRMU5P1QKOUNMy
Lvp58brdyXaUgCIcIFEHzBAT6POZFLqIb+wSPeJzrlunzeW7IWxsj43380iGpijwt3gYzy
Lu08asFrQF/m+uAvuilxC2nbC4LpEATi6Z/tr8+BqXZLKvCrdwxkXhaabBZTDZ3uFG287V
hUbFXmy4rdAWIJN7TLS8etxlnCkP3Dao7LQlAtXZb8/eLINqOejDiT+QdNIcCzc/T+SQAA
AMBfnEHQ6H1FyGKWYK2vTuC7jKAaAxLamJ+TNTzdpCrZIBk+9j9FRt9oQFSokuU+rW5vlM
RIgkHZ/1KpsGL5WR3lx8UVRxMQSj/N5sQqs94W0YU7Ku+zOJrME2U9HsD4sGZrThKXz7Vp
6wDm5FFfZe+Xty4oyCBvxc/IZojGZY8ts+m4T6O9eQPAEPJ4RBH+pwDntX5Fsj5/3VxGrJ
GfAKEL8jEgzSKEe43HKQelFlhZl/H5RVnVKYpbbKsoUhMLkkMAAADBAOTvRkg5gBtPF21J
M5q+fDPIBlXboclTDC0UiGEh5Y82trHN+vi2fzNpqmU8t3fovo27b1M9tuHAUoliu4NO8W
v8PrXOTPDTY6okc8CCFHhUCxKsTiWA/EudAj7RuVqMyDdEK43sqZhUPoxWkbYZ0map4ryx
sMftkZEL3ZHvCRdR2bt2Sc5pXLTvfX3X02i5IzABuAvVG4yhXuEPrhgANuWR6cB+9pRVTi
RHjf5G+VkpvpuiRFKXfBHtNoEwTGN5jwAAAMEAxZ0TrjrSz+XDm+r2QEUvKHG06i0Xv3VP
moqgnrq3GyogMYBcQPMY6woVsBlMrf9vTkqM+DjENHEHu2ZvH/Sfy4qI3NYArTi9bDYRnp
KaP9UzkTce5yj374uYI6RLVI8VOX65OPr8ifv+o3bU+ppKcawDHyzZPSj06Fe5/IvJ5Ovo
zLmagUlFCbu7F+FFkAiaJopjxrChTijg7a54ou57blFMO7KQL7hv6HN5XEvyyJAwCti0Wa
hokSgOriX8OuITAAAACmpvaG5AeHBzMTU=
-----END OPENSSH PRIVATE KEY-----root@kali:~/Downloads#
```

* Use any text editor add a extra line  after `-----END OPENSSH PRIVATE KEY-----` line. Usually private key file should only be readable by its owner. Therefore, changing the permissions of the id_rsa file to 600 and sshing in, we can read the flag.txt.

```
root@kali:~/Downloads# chmod 600 id_rsa 
root@kali:~/Downloads# ssh -i id_rsa user@jh2i.com -p 50004
user@9e79ac95822a:~$ ls
flag.txt
user@9e79ac95822a:~$ cat flag.txt 
flag{dont_ever_forget_that_newline}user@9e79ac95822a:~$ logout
Connection to jh2i.com closed.
root@kali:~/Downloads#
```

## Flag
```
flag{dont_ever_forget_that_newline}
```
