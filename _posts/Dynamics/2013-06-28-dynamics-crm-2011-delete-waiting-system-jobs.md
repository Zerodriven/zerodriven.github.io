---
layout: single
date:   2013-06-28 13:21:00 +0100
categories: Dynamics CRM
tags: [DynamicsCRM, SQL]
---

Situation:

Working with a fellow CRM techie on a very tricky CRM issue where campaign signups where triggering workflows, and leaving them in a ‘Waiting’ state, never moving (After monitoring them all for a week) – Attempting to bulk delete them wouldn’t work, saying you cannot delete an active workflow. Obviously, waiting till the 30th of December year 9999 is something not many people will have patience for and the waiting was causing a resourcing issue on the VM it was hosted on.

With all the supported options not working or not viable (350,000+ records at 250 a go = not viable), the only step left was SQL. Now, the following solution is unsupported and it is not recommended unless you have backups. This solution is ‘as is’ and could change in the future and we will not be made liable for issues that this could cause in your Microsoft Dynamics 2011 system. Just a nice warnng..

Solution:

Thanks to Amit for writing this SQL with me watching over Lync, note: Numbers are taken from the MS Dynamics SDK and the Regarding it taken from the campaign. We needed a full wipe on anything, so that’s why we were specific:

```sql
USE [DATABASE]

delete from WorkflowLogBase
where AsyncOperationId IN
(Select AsyncOperationId from AsyncOperationBase
where StatusCode= 10 and
StateCode= 1 and
RegardingObjectIdName = ‘REGARDINGNAME’
);
```


```sql
USE [DATABASE]

delete from AsyncOperationBase
where StatusCode= 10 and
StateCode= 1 and
RegardingObjectIdName = ‘REGARDINGNAME';
```
