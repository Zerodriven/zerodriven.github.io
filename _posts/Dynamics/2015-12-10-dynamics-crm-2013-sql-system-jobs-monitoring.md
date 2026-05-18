---
layout: single
date:   2013-06-28 13:21:00 +0100
categories: Dynamics CRM
tags: [DynamicsCRM]
---

Last one for today.. Another instance of me using SSRS to send me emails every day, just so I can keep track of system wide errors. Nice for workflows and custom code we use internally which fails. Obviously half of them I have to source to our developers.. But, information is useful.


```SQL
SELECT CreatedOn, Name, FriendlyMessage, Message, RegardingObjectIdName, OwningExtensionIdName   FROM [INV_MSCRM].[dbo].[AsyncOperationBase]   WHERE FriendlyMessage is not null and CreatedOn >= getDate() - 1
   order by createdon desc`
```
