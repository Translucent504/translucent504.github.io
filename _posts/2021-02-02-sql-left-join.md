---
title: "SQL LEFT JOIN with an extra condition"
excerpt_separator: "<!--more-->"
categories:
  - today-i-learned
tags:
  - til
---

> SQL LEFT JOIN with an extra condition.

<!--more-->

# tl;dr Solution:

**Put the condition with the JOIN's ON clause rather than in the WHERE clause**

Do this:
```sql
SELECT
  cl.Id,
  cl.Name,
  cla.Submit,
  cla.Link,
FROM
	CheckList AS cl
LEFT OUTER JOIN CheckListAdmins AS cla ON
	cl.ChkID = cla.ChkID AND cla.GrNo = 1234
WHERE
	cl.Type = 3
```

Not something like this:
```sql
SELECT
  cl.Id,
  cl.Name,
  cla.Submit,
  cla.Link,
FROM
	CheckList AS cl
LEFT OUTER JOIN CheckListAdmins AS cla ON
	cl.ChkID = cla.ChkID 
WHERE
	cl.Type = 3 AND (cla.GrNo = 1234 OR ...??? OR ....??)
```

# Problem: 

I have 2 tables:
  1. Checklist
  2. ChecklistAdmins

Checklist has a list of items with Ids. ChecklistAdmins contains records for whenever a person (identified by a grNo) submits one of the items from the checklist.  
I wanted a single query that returns to me whether a certain person has submitted all items of a certain type or not. In this case it will return null for the fields of the checklist that the person hasnt submitted, which is what I want.
