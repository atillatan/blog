---
layout: article
title: SQL table data compare, and prepare insert satements
description: SQL table data compare, and prepare insert satements
comments: true
sortorder: 150
---

# DATA Compare
```sql

--Compare result1,
select * from
( SELECT  * FROM [80.123.40.123].[CIMS.Settings].[dbo].[Resource] ) a
right join (SELECT  * FROM  [CIMS.Settings].[dbo].[Resource] ) b
on a.Code=b.Code and a.Culture = b.Culture
where a.No is null


--Compare result2,
select * from
( SELECT  * FROM [80.123.40.123].[CIMS.Settings].[dbo].[Resource] ) a
left join (SELECT  * FROM  [CIMS.Settings].[dbo].[Resource] ) b
on a.Code=b.Code and a.Culture = b.Culture
where b.No is null



--Prepare INsert SQL


select 'INSERT INTO [dbo].[Resource]([Culture], [Code], [Value], [IsEditable])   VALUES('''+b.Culture+''' ,'''+b.Code+''' ,'''+b.[Value]+''' ,0)'  from
( SELECT  * FROM [80.123.40.123].[CIMS.Settings].[dbo].[Resource] ) a
right join (SELECT  * FROM  [CIMS.Settings].[dbo].[Resource] ) b
on a.Code=b.Code and a.Culture = b.Culture
where a.No is null


select 'INSERT INTO [dbo].[Resource]([Culture], [Code], [Value], [IsEditable])   VALUES('''+a.Culture+''' ,'''+a.Code+''' ,'''+a.[Value]+''' ,0)'  from
( SELECT  * FROM [80.123.40.123].[CIMS.Settings].[dbo].[Resource] ) a
left join (SELECT  * FROM  [CIMS.Settings].[dbo].[Resource] ) b
on a.Code=b.Code and a.Culture = b.Culture
where b.No is null


```
