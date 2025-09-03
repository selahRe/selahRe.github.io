---
date: '2025-09-03T16:03:40-04:00'
draft: true
title: 'Arithmetic'
lastmod: 2025-09-03T16:03:40-04:00

categories:
- Arithmetic

tags:
- 算法

url: "/about/"
summary: "search"
layout: "search" # necessary for search

description: "算法" # 文章描述，与搜索优化相关
summary: "算法" # 文章简单描述，会展示在主页
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
递归 recursion：
https://www.bilibili.com/video/BV1LiS1YSEgF/ **将fuction看作答案**
```java
//1. 确定问题 汉诺塔问题 有什么参数 n个圆盘从From柱子借用Assist柱搬到To柱，此时将函数看作答案
void hanoi(int n, char F, char A, char T){
  //2.
  //3.
  }
// 2. 什么时候直接计算返回
  if( n == 1){
    System.out.println("move %d from %c to %c\n", n, F, T);
    return;
  }
// 3. 如果是n怎么用n-1解决（3->2->1）
  hanoi(n-1, F, T, A); //让n-1个圆盘从F到在A柱子
  System.out.println("move %d from %c to %c\n", n, F, T);
  hanoi(n, A, F, T) //让n-1个圆盘都从A放到T柱子
```
dfs深度搜索
二叉树
dfs图论
例子：797. 所有可能的路径 https://leetcode.cn/problems/all-paths-from-source-to-target
```java
//输入：graph = [[1,2],[3],[3],[]] 输出：[[0,1,3],[0,2,3]]
//1. 写函数
int[][] graph //图 
List<List<Integer>> ans = new ArrayList<>(); //保存所有路径
List<Integer> cur = new ArrayList<>(); //保存单一路径
public List<List<Integer>> allPathsSourceTarget(int[][] graph) {
        g = graph;
        cur.add(0);
        dfs(0);
        return ans;
    }
void dfs (int node) {//目前搜索的节点
    //2.
    //3.
  }
//2. 什么时候直接计算返回 ->到最终节点即答案
if( node == graph.length-1){
  ans.add(new ArrayList<>(cur)); //存放结果
  return;
}
//3. 处理目前node出发的路径
for(int i : graph[node]){
    cur.add(i); //加从node出发节点后
    dfs(i); //处理节点
    cur.remove(cur.size() - 1); //回溯删除这个节点 [0,1].size() = 2
  }
```

