---
layout: post
title:  "sql存储引擎对比"
date:   2018-03-07 10:22:18 +0800
categories: emacs
---

# 动机
判断数据量多时，那种存储引擎查询比较快
# 步骤
数据总数 300万条 占用磁盘空间 1G 左右

#数据结构

表1 news [ 文章表 引擎 myisam 字符集 utf-8 ]
-----------------------------------------------------
```sql
id	int	11	主键自动增加
cate	int	11	索引
title	varchar	200	标题(便于基础搜索做了索引)
content	text		文章正文
date	int	11	文章发布时间(时间戳形式)

```
表2 cate [ 文章分类表 引擎 myisam 字符集 utf-8 ]
-----------------------------------------------------
```sql
cate_id		int	11	主键自动增加
cate_name	varchar	200	文章标题


查询总数

myIsam 引擎下
select count(*) as total from news
//耗时 0.001秒 极快 

//带上条件
select count(*) as total from news where cate = 1
耗时 0.046秒 可以接受的速度

innodb 引擎下
select count(*) as total from news
//耗时 0.7秒 很慢
select count(*) as total from news where cate = 1
耗时 0.7秒 很慢

```


#为什么2种引擎查询速度相差这么大？
InnoDB 中不保存表的具体行数，也就是说，执行select count(*) from table时，InnoDB要扫描一遍整个表来计算有多少行。
MyISAM只要简单的读出保存好的行数即可。
注意的是，当count(*)语句包含 where条件时，两种表的操作有些不同，InnoDB类型的表用count(*)或者count(主键)，加上where col 条件。其中col列是表的主键之外的其他具有唯一约束索引的列。这样查询时速度会很快。就是可以避免全表扫描。
#总结
mysql 在300万条数据（myisam引擎）情况下使用 count(*) 进行数据总数查询包含条件（正确设置索引）运行时间正常。对于经常进行读取的数据我们建议使用myIsam引擎



------------------------------------------------------------------------------

