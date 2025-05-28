---
date: '2025-03-13T16:16:58+08:00'
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
=======
git add content/post/*.md
git status //变绿，已添加到
git commit -m “描述此次做了什么” 
git push
git push --force origin main //强制合并
git push -u origin xxx//分枝
>>>>>>> recover-md-files
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
<<<<<<< HEAD
cd ... in **terminal** and git commit -m "Initial Commit"
=======
cd ... in **terminal** and git commit -m "Initial Commit"
## 上传到分枝
```
git init
 git remote -v //检查是否用ssh连接
ssh -T git@github.com
git remote add origin https://github.com/name/project.git
git remote set-url origin git@github.com:name/project.git
git branch //查看分枝
git checkout -b xxx //新建
git add . 
 git commit -m "add project"
git push -u origin xxx 
```
## Git 修改历史 Commit message

```
git rebase -i --root //修改第一个
git commit --amend //最近一条
git log //查看全部
git rebase -i 8876a66df1ea4a7e911c271b2bd3292ddfa1eca0 //修改指定commit即其之后的
//reword：保留该 commit，但我需要修改该commit的 Message
reword xxxxx new commit
```

