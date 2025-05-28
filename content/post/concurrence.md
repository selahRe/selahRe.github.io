---
date: '2025-03-05T02:10:17+08:00'
draft: true
title: 'Concurrence'
lastmod: 2025-03-05T02:10:17+08:00

categories:
- java
- Concurrence

tags:
- 八股

description: "" # 文章描述，与搜索优化相关
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
多线程不安全演示
```java
new CountDownLatch(50);
```

客户端 TCP socket建立连接
```C++
void main(int argo, char *argvl])//需要传入服务器域名和端口号
｛
struct sockaddr_in sad; /* structure to hold an IP address of server */ 
int clientSocket; /* socket descriptor */
struct hostent *ptrh; /* pointer to a host table entry *y*/
char Sentence[128];
char modifiedSentence[128];
host = argv[1]; //服务器域名 String，argv[0]执行程序名字
port = atoi(argv[2]);//服务器端口号转成Integer
//Create client socket, connect to server
clientSocket = socket(PF_INET, SOCK_STREAM, 0);//PF_INET intern地址组建；SOCK_STREAM TCP的socket
memset((char *)&sad,0,sizeof(sad)); /* clear sockaddr structure 给sad清零 */
//给sad赋值
sad.sin_family = AF_INET; /* set family to Internet */
sad.sin_port = htons((u_short)port);//u_short短整型无符号的；htons网络次序？？？
//struct hostent *ptrh; 
hostent ptrh = gethostbyname(host); /* Convert host name to IP address */
memcpy(&sad.sin_addr, ptrh->h_addr, ptrh->h_length);//将IP地址拷贝到sad.sin_addr
connect(clientSocket, (struct sockaddr *)&sad, sizeof(sad));//建立连接
gets(data);
n = write(clientSocket, data, strlen(data)+1);
close(clientSocket);
```
Server TCP socket
```C++
void main(int argo, char *argvl]){
struct sockaddr_in sad; /* structure to hold an IP address of server*/ 
struct sockaddr_in cad; /*client */
int welcomeSocket, connectionSocket; /* socket descriptor */ 
struct hostent *ptrh; /* pointer to a host table entry */
char clientSentence[128];
char capitalizedSentence[128];
port = atoi(argv[1]);
//Create welcoming socket at port & Bind a local address
welcomeSocket = socket(PF_INET, SOCK_STREAM, 0);
    memset((char *)&sad,0,sizeof(sad)); /* clear sockaddr structure */
    sad.sin_family = AF_INET; /* set family to Internet */
    sad.sin_addr.s_addr = INADDR_ANY; /* set the local IP address */
    sad.sin_port = htons((u_short)port);/* set the port number */
bind(welcomeSocket, (struct sockaddr *)&sad, sizeof(sad));
/* Specify the maximum number of clients that can be queued */
listen(welcomeSocket, 10);//连接后还要其他的连接请求，把请求放在队列中
while (1) {
//Wait, on welcoming socket for contact by a client
connectionSocket=accept(welcomeSocket, (struct sockaddr *&cad, &alen);
n=read(connectionSocket, clientSentence, sizeof(clientSentence));
/* capitalize data and store the result in data*/
n=write(connectionSocket, data, strlen(data) + 1);//Write out the result to socket
close(connectionSocket);//End of while loop, loop back and wait for another client connection
}
}
```


















