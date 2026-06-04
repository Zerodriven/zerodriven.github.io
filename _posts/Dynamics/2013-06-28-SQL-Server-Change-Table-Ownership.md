---
layout: single
date:   2013-06-28 13:21:00 +0100
categories: Dynamics CRM
tags: [SQL]
---


We’ve got a 3rd party application we’re having to upgrade which generates tables on the fly, the issue with this is that the database owner (Which should be DBO) is actually the user’s domain account, e.g. XXX\JasonB.TableName.

The script below will fix it, run it on any database where you need to change table schema names to DBO. The script will print out (on a per-line basis) some SQL to run which will sort it.

```SQL
ELECT 'ALTER SCHEMA dbo TRANSFER ' + QUOTENAME(TABLE_SCHEMA) + '.' + QUOTENAME(TABLE_NAME)   FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_SCHEMA = 'XXX\jasonb'
```

Remember to change the domain name! 🙂