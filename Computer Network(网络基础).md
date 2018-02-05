# 网络基础：
## 1.TCP和UDP的区别
TCP：面向连接、传输可靠(保证数据正确性,保证数据顺序)、用于传输大量数据(流模式)、速度慢，建立连接需要开销较多(时间，系统资源)。
UDP：面向非连接、传输不可靠、用于传输少量数据(数据包模式)、速度快。
## 2.TCP三次握手四次挥手
  
  三次握手
 
      第一次握手：建立连接。客户端发送连接请求报文段，然后，客户端进入SYN_SEND状态，等待服务器的确认；
      第二次握手：服务器收到SYN报文段。SYN报文段进行确认；同时，自己还要发送SYN请求信息；服务器端将上述所有信息放到一个报文段（即SYN+ACK报文段）中，一       并发送给客户端，此时服务器进入SYN_RECV状态；
       第三次握手：客户端收到服务器的SYN+ACK报文段,客户端进入established状态。然后向服务器发送ACK报文段，这个报文段发送完毕以后，服务器端进入    
        ESTABLISHED状态，完成TCP三次握手。

  四次分手：

      第一次分手：主机1（可以使客户端，也可以是服务器端）向主机2发送一个FIN报文段；此时，主机1进入FIN_WAIT_1状态；这表示主机1没有数据要发送给主机2了；
      第二次分手：主机2收到了主机1发送的FIN报文段，向主机1回一个ACK报文段；主机1进入FIN_WAIT_2状态；主机2告诉主机1，我“同意”你的关闭请求；
      第三次分手：主机2向主机1发送FIN报文段，请求关闭连接，同时主机2进入LAST_ACK状态；
      第四次分手：主机1收到主机2发送的FIN报文段，向主机2发送ACK报文段，然后主机1进入TIME_WAIT状态；主机2收到主机1的ACK报文段以后，就关闭连接；
      此时，主机1等待2MSL后依然没有收到回复，则证明Server端已正常关闭，那好，主机1也可以关闭连接了。

## 3.什么是后端服务器
1)本质：是向前端提供需要显示网页和APP内容的数据，可能是HTML，也可能是JSON数据，也可以是音视频或者PDF文件。
2)一个服务器包含3个部分：

* HTTP服务器：

      把（需要返回给客户端的）资源文件封装在HTTP数据包里；这个资源有可能是它后面的应用服务器动态生成的，
      也有可能是保存在硬盘上的静态文件；
      这个资源是所有后端程序都必须有的，也是直接和我们的浏览器通信，返回给我们数据的程序；

      这个资源作用就是把它（后面的编程语言生成的各种HTML/CSS/Javascript），打包成一个HTTP请求，然后再封装到一个TCP/IP的数据包里发回给浏览器端；

      最常用的两个HTTP服务器叫做Apach和Nginx。

* 应用服务器：生成前端需要的HTML/CSS/JS交给浏览器
* 数据库

(原文链接：https://www.jianshu.com/p/69f1553b7714)

## 4.访问www.google.com的时候发生了什么？

1) 流程概述：
  
  a）浏览器会自动补全为http://www.google.com/, 这是个url,他表示网络某个资源(resource)的位置, 
  一般格式为: protocol :// hostname[:port] / path / ;parameters#fragment

  b)浏览器拿着这个domain找离你最近的DNS，DNS是网络运营商(电信,联通,移动,verizon,comcast)提供的。DNS服务器返回给我一个IP地址.
  浏览器向这个IP地址发送一个http/https Request, google的服务器处理这个请求之后返回对应的Response，是一个html文件，浏览器将html文件显示.

2) Google的服务器端：

a)Google的Web Server(硬件)收到request，将这个request递交给正在80端口监听的HTTP Server(跑在Web Server上的软件，常见的有Nginx,Apache,Unicorn,Gunicorn等)，80端口是专为http开放的，端口号用来区分这台主机提供的不同服务，由TCP/IP协议栈规定.

 b)HTTP拿到request后转发给Web Application(我们写的程序)，常见框架:Django(Python),Ruby on Rails(Ruby),NodeJS(JS),Dropwizard(Java).
应用服务器把写好的html+css+js通过http协议发回给浏览器，浏览器显示并运行这些文件，以此页面为出发点，开始后续的交互.
(原文：https://segmentfault.com/a/1190000006129691)
