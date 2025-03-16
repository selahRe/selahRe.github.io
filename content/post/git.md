---
date: '2025-03-13T16:16:58+08:00'
draft: true
title: 'Git'
lastmod: 2025-03-13T16:16:58+08:00

categories:
- how to use
tags:
- git

description: "git" # 文章描述，与搜索优化相关
summary: "" # 文章简单描述，会展示在主页
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
## 上传更改
```java
git status //什么改变了
git add .
git status //变绿，已添加到
git commit -m “描述此次做了什么” 
git push
```
## IDEA 中使用 git
.gitignore --> ignore some documents
```java
**/target/
.idea
*.iml
*.class
*Test.java
**/test/
```
1️⃣**IDEA**-VCS-create git repository - commit
2️⃣new a repository in your **github** and copy the http link
3️⃣**IDEA** push-define remote (auto create a master branch)
if master-> Empty repository
cd ... in **terminal** and git commit -m "Initial Commit"