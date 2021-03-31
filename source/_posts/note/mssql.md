---
title: SQL Server 笔记
date: 2021-03-31 13:47:37
tags:
- sql
- mssql
categories:
- 零散笔记
---

## 分组排序
```
ROW_NUMBER() OVER(PARTITION BY COL1 ORDER BY COL2)
```
比如，把每个班的学生按年龄从小到大的排序：
<!--more-->

```
SELECT
    [CLASS]
   ,[NAME]
   ,[AGE]
   ,ROW_NUMBER() OVER (PARTITION BY [CLASS] ORDER BY [AGE] ASC)
FROM TEST_T
```

## Merge
简单使用：如果学生信息存在，则更新学生年龄。如果不存在，则插入学生信息。
```
MERGE INTO D_StudentT AS target
USING Temp_StudentT AS source
    ON target.CLASS = source.CLASS 
    AND target.NAME=source.NAME
WHEN MATCHED THEN
    UPDATE SET target.AGE=source.AGE,
               target.UpdatedTime=GETDATE()
WHEN NOT MATCHED THEN
    INSERT(CLASS,NAME,AGE) 
    VALUES(source.CLASS,source.NAME,source.AGE);
```