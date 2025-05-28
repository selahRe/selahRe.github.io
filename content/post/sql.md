---
date: '2025-03-20T09:13:23+08:00'
title: 'Sql'
lastmod: 2025-03-20T09:13:23+08:00

categories:
- project 
- sql

tags:
- sql

url: "/about/"
summary: "sql"
layout: "sql" # necessary for search

description: "" # 文章描述，与搜索优化相关
weight: # 输入1可以顶置文章，用来给文章展示排序，不填就默认按时间排序
slug: ""
draft: false # 是否为草稿
comments: true
showToc: true # 显示目录
TocOpen: true # 自动展开目录
autonumbering: true # 目录自动编号
hidemeta: false # 是否隐藏文章的元信息，如发布日期、作者等
disableShare: true # 底部不显示分享栏
searchHidden: false # 该页面可以被搜索到
showbreadcrumbs: true #顶部显示当前路径
mermaid: true
cover:
    image: ""
    caption: ""
    alt: ""
    relative: false
---
## 在终端打开mysql 登录/导入/导出
```java
source ~/.bash_profile
//登录使用
mysql -u root -p 
mysql> show databases;
//导出database数据
mysqldump -u root -p game>game.sql
//create database game;后再导入
mysql -u root -p game<game.sql
```
create a database and use
### 创建table
在Navicat中连接并进入database game，New Query 可输入命令行
```sql
create database game;
use game;
CREATE TABLE player(
	id INT, -- int/float/double
	name VARCHAR(10), --char/varchar/text/blob 定长/变长/文本/二进制数据
	LEVEL INT, --还有日期和时间类型 date/time/datetime/timestamp 时间戳
	exp INT,
	gold DECIMAL(10,2) --长度10并保留2位数小数的十进制数值
)
desc player --查看table的结构
```
### 修改table
```sql
/*
COLUMN 可省略：修改列默认值等
不可：修改列名/类型/删除列/加新列
*/
ALTER TABLE player modify COLUMN name VARCHAR(20);
ALTER TABLE player modify COLUMN name to nick_name;
ALTER TABLE player add COLUMN last_login TIMESTAMP;
ALTER TABLE player drop COLUMN last_login;
--drop table player;
--drop database game;
```
列的约束：DEFAULT/unique/null/not null/
主键约束：数据唯一性，不为空
外键约束：数据一致性，外键必须是另一个table的主键
## 增删改查
```sql
--增
ALTER TABLE player modify LEVEL INT DEFAULT 1;--unique/null/not null
INSERT INTO player (id, name, level, exp, gold) VALUES(1,'Lily',1,1,1);
INSERT INTO player (id, name) VALUES(2,'Shiv'); --其他用默认值填充
INSERT INTO player (id, name) VALUES(3,'Sam'), (4,'Logan');
--改
UPDATE player set LEVEL = 2 WHERE name = 'Lily';
UPDATE player set exp = 0, gold = 0;--修改所有的
--删
DELETE FROM player WHERE id = 1;
--查 nor>and>or或者用（）
SELECT * from player where LEVEL>=1 and LEVEL<=10;
SELECT * from player where level between 1 and 10;
SELECT * from player where LEVEL in (1,3); --1/3
SELECT * from player where name like '%王%';
SELECT * from player where name regexp '王';--和上面相同
SELECT * from player where name regexp'^王.$';--查找王x
--查找空
SELECT * from player where email is null; --非空 is not null
SELECT * from player where email = '';--空字符串
```
### where/ between and/ in
### 模糊查找 
like %任意n个字符 _任意1个字符
regexp 正则表达式
| 表达式 | 含义 |
|  ----  | ----  |
| .  | 任意一个字符 |
| ^  | 开头 | 
| $  | 结尾 | 
| [abc]  | 其中任意一个字符 | 
| [a-f]  | 范围内任意一个字符 | 
 A｜B  A或者B 
### 排序 order
```sql
SELECT * from player order by level;--升序 ASC
SELECT * from player order by level DESC, exp;--level降序基础上用exp升序排列
```
## 计算
聚合函数
| 表达式 | 含义 |
|  ----  | ----  |
| AVG( ) | 平均值 |
| count( )  | 项目数 | 
| max( ) | max | 
| min( ) | min | 
| sum( ) | sum| 
 ```sql
SELECT count(*) from player;
SELECT avg(level) from player;
```
### 分组
 ```sql
SELECT sex, count(*) from player group by sex; --count (sex) 不计算null的数量
SELECT level, count(level) from player group by level HAVING COUNT(level)>4; -- 同一个level人数>4的
SELECT SUBSTR(name, 1, 1), COUNT(SUBSTR(name, 1, 1)) from player
GROUP BY SUBSTR(name, 1, 1)
HAVING COUNT(SUBSTR(name, 1, 1))>4 ORDER BY COUNT(SUBSTR(name, 1, 1)) DESC;--统计姓氏降序排
```
限制输出(**分页**效果）
```sql
limit 3; --输出前3个
limit 3, 3; --输出前4-6个
```
### 去重distinct
```sql
SELECT distinct sex from player; 
```
### 两个select一起查找 Union
```sql
--合并并集，只查出一次
SELECT * from player where LEVEL in (1,3)
Union
SELECT * from player where exp between 1 and 3;
-- Union all 不合并
```
## 子查询
用前面的查询作为先决条件
```
insert into new_player select * from player where level >5;
select exists()
```
## 表关联
关联的表里面有相同字段，用表的主键和外键关联
### 内连接
```
SELECT * from player
INNER JOIN equip  --用inner join指定关联的表
on player.id = equip.player_id; --on +关联字段
```
left join 显示左表完整的信息，右表没有相关的就用null填充
right join
```
SELECT * from player p, equip e
where  p.id = e.player_id;
```
## 索引
CREATE [UNIQUE|FULLTEXT|SPATIAL] INDEX index_name;
唯一/全文/空间 索引名称 
on 哪张表（哪些字段）创建索引
```
CREATE INDEX id_index ON player(id);
show INDEX FROM player;
drop INDEX id_index on player; --删除
alter table player add index id_index (id);
```
## 视图
```
--新建
CREATE VIEW top
as 
SELECT * from player ORDER BY LEVEL desc LIMIT 10;
--修改
alter VIEW top
as 
SELECT * from player ORDER BY LEVEL LIMIT 10;
--查看
SELECT * from top 
--删除
drop view top;
```









