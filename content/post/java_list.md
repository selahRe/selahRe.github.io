---
date: '2025-03-04T14:58:32+08:00'
title: 'Java_list'
lastmod: 2025-03-04T14:58:32+08:00

categories:
- java

tags:
- java


description: "java基础" # 文章描述，与搜索优化相关
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
## 1.  array
新建array 
```java
int[] arr = new int[len];//default 0
```
初始化array 
```java
Arrays.fill(arr, -1);//init -1
```
## 2.  hashMap
```java
HashMap<Integer, Integer> map = new HashMap<>();
map.put(nums1[i], i);
if (map.containsKey(nums1[i])) {
   map.get(nums1[i])//==i; 
   }
```
## 3.  Stack
```java
Stack<Integer> stack = new Stack<>();
stack.push(num);//stack.pop(), stack.peek()
//stack.isEmpty()
Deque<Integer> stack = new LinkedList<>();
stack.push(0);
```
## 泛型
非static
```java
class 类名称 <泛型标识> {
  private 泛型标识 /*（成员变量类型）*/ 变量名; 
  .....

  }
}
```
如果static
```java
public class Test2<T> {   
	// 泛型类定义的类型参数 T 不能在静态方法中使用  
    public static <E> E show(E one){ // 这是正确的，因为 E 是在静态方法签名中新定义的类型参数    
        return null;    
    }    
}  
interface IUsb<U, R> {

    int n = 10;
    U name;// 报错！ 接口中的属性默认是静态的，因此不能使用类型参数声明
    R get(U u);// 普通方法中，可以使用类型参数
    void hi(R r);// 抽象方法中，可以使用类型参数
    // 在jdk8 中，可以在接口中使用默认方法, 默认方法可以使用泛型接口的类型参数
    default R method(U u) {
        return null;
    }
}

```
## 迭代和递归
1、确定递归函数的参数和返回值
2、确定终止条件
3、确定单层递归的逻辑
递归回溯dfs






















