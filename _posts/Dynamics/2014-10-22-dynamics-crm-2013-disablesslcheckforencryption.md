---
layout: single
date:   2013-06-28 13:21:00 +0100
categories: Dynamics CRM
tags: [DynamicsCRM]
---

– Open SQL Server MGMT Studio  
– New Query:


```sql 
SELECT *   FROM DeploymentProperties   WHERE ColumnName = 'DisableSSLCheckForEncryption'  UPDATE DeploymentProperties   SET BitColumn = 1   WHERE ColumnName = 'DisableSSLCheckForEncryption'  SELECT *   FROM DeploymentProperties   WHERE ColumnName = 'DisableSSLCheckForEncryption'   `

`--COMMIT   --ROLLBACK  
USE MSCRM_CONFIG
BEGIN TRAN

```

Restart IIS after. You’ll now be able to enable data encryption.