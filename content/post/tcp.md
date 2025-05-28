---
date: '2025-03-21T06:01:06+08:00'
title: 'Tcp'
lastmod: 2025-03-21T06:01:06+08:00

categories:
- network
- java

tags:
- network
- java

summary: "tcp"
layout: "tcp" # necessary for search

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
### 原理
第一次通讯中等待连接的程序被称为服务器端(Sercer)程序，利用IO流实现数据的传输
1、在服务端指定一个端口号来创建ServerSocket，并使用accept方法进行侦听，这将阻塞服务器线程，等待用户请求。
2、在客户端指定服务的主机IP和端口号来创建socket，并连接服务端ServerSocket，此时服务端accept方法被唤醒，同时返回一个和客户端通信的socket。
3、在客户端和服务端分别使用socket来获取网络通信输入/输出流，并按照一定的通信协议对socket进行读/写操作。
4、通信完成后，在客户端和服务端中分别关闭socket
## 客户端
```java
Socket(InetAddress address, int port)	//创建流套接字并将其连接到指定IP地址的指定端口号
Socket(String host, int port)	//创建流套接字并将其连接到指定主机上的指定端口号
utputStream getOutputStream()	//返回此套接字的输出流
InputStream getInputStream()	//返回此套接字的输入流
void shutdownOutput()	//禁用此套接字的输出流

public class ClientDemo {
    public static void main(String[] args) throws IOException {
        // 创建客户端的Socket对象(Socket)
        // Socket(InetAddress address, int port): 创建流套接字并将其连接到指定IP地址的指定端口号
//        Socket s = new Socket(InetAddress.getByName("127.0.0.1"), 10005);
        // Socket(String host, int port): 创建流套接字并将其连接到指定主机上的指定端口号。
        Socket s = new Socket("127.0.0.1", 10005);

        // 获取输出流，写数据
        // OutputStream getOutputStream(): 返回此套接字的输出流。
        OutputStream os = s.getOutputStream();
        os.write("Java YYDS!".getBytes());
        // 接收服务器反馈
        InputStream is = s.getInputStream();
        byte[] bys = new byte[1024];
        int len = is.read(bys);
        String data = new String(bys, 0, len);
        System.out.println("客户端：" + data); 
        // 释放资源
        s.close();
    }
}
```
## 服务器
```java
ServerSocket(int port); \\创建服务器端的Socket对象(ServerSocket)
Socket accept(); \\获取输入流，读数据，并把数据显示在控制台

public class ServerDemo {
    public static void main(String[] args) throws IOException {
        // 创建服务器端的Socket对象(ServerSocket)
        ServerSocket ss = new ServerSocket(10005);

        // Socket accept(): 侦听要连接到此套接字并接受它
        Socket s = ss.accept();

        // 获取输入流，读数据，并把数据显示在控制台
        InputStream is = s.getInputStream();
        byte[] bys = new byte[1024];
        int len = is.read(bys);
        String data = new String(bys, 0, len);
        System.out.println("数据是：" + data);

        // 释放资源
        ss.close();
    }
}

```