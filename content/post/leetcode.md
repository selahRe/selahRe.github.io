---
date: '2025-03-04T15:45:56+08:00'
draft: true
title: 'Leetcode'
lastmod: 2025-03-04T15:45:56+08:00

categories:
- java

tags:
- leedcode

url: "/about/"
layout: "search" # necessary for search

description: "java, leedcode" # 文章描述，与搜索优化相关
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
## 处理循环数组
- 把两个数组拼接在一起
- 循环两次
```java
for(int i = 0; i < 2*size; i++) //nums[i % size]
```