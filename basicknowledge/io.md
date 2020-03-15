# IO

## IO 基础编程:

### 1. 简介:

  IO 分为两类: java.io中阻塞流和java.nio中非阻塞流。  
   $\color{YellowGreen}{阻塞流}$：面向流操作的。  
    从流中读取数一个字节或者多个字节，直至读完所有的字节，没有任何缓存的地方。还不能移动流中的数据，如果想要操作数据，需要将数据写入到缓存中进行处理。  
     java io 的各种流的操作都是阻塞的, 当在线程调用 read\(\)或者writer\(\)时,该线程被阻塞,直到数据完全操作完成才能操作其他的事情。  
   $\color{YellowGreen}{非阻塞流}$: 面向缓冲区。將数据直接放入缓存中,可以直接操作数据,但是在操作数据之前,需要查看缓存中是否有需要处理的数据。而且在处理数据时需要注意的是不能将没处理的数据处理了。  
     java io 非阻塞模式,式一个线程从某个通道发起请求时,只能操作当前缓存中的数据,如果没有数据处理,就什么也不会操作,所以当数据还没处理完成之前可以操作缓存中的数据,当一个线程写入数据时,不需要等他全部写入就可以操作数据了。

TODO: NIO 选择器概念?

### 2. 处理数据:

   如果纯粹的使用 nio 设计相较于 io 设计,数据处理方面比较麻烦:  
   $\color{YellowGreen}{java-io :}$

```text
Name: Anna 
Age: 25
Email: anna@mailserver.com 
Phone: 1234567890
```

   处理过程:

```text
InputStream input = ... ; // get the InputStream from the client socket   

BufferedReader reader = new BufferedReader(new InputStreamReader(input));   

String nameLine   = reader.readLine(); 
String ageLine    = reader.readLine(); 
String emailLine  = reader.readLine(); 
String phoneLine  = reader.readLine();
```

当执行完nameLine readLine\(\) 方法时,你会知道一行数据被处理完了,因为 readLine\(\) 会一直阻塞,直到数据被处理完成。一旦数据被处理完成，就不能再次进行处理。

   $\color{YellowGreen}{java-nio:}$

```text
ByteBuffer buffer = ByteBuffer.allocate(48); 
int bytesRead = inChannel.read(buffer);
```

当执行 read\(buffer\) 时,你不知道需要处理的数据是否已经进入缓存中,比如: 当数据存到缓存中是 Name: An 这个时候对数据操作是没有意义的,这个时候就会去缓存中查看数据是否已经完整的存到缓存中。这样的操作使程序的设计异常的复杂。

### 3. 明细:

   $\color{YellowGreen}{IO中输入字符流:}$

> Reader
>
> > CharArrayReader  
> > FilterReader  
> > PushbackReader  
> > InputStreamReader  
> > FileReader  
> > PipedReader  
> > StringReader  
> > BufferedReader
> >
> > > LineNumberReader

1. Reader是所有的输入字符流的父类，它是一个抽象类。   
2. CharReader、StringReader是两种基本的介质流，它们分别将Char数组、String中读取数据。PipedReader是从与其它线程共用的管道中读取数据。   
3. BufferedReader很明显就是一个装饰器，它和其子类负责装饰其它Reader对象。   
4. FilterReader是所有自定义具体装饰流的父类，其子类PushbackReader对Reader对象进行装饰，会增加一个行号。     
5. InputStreamReader是一个连接字节流和字符流的桥梁，它将字节流转变为字符流。FileReader可以说是一个达到此功能、常用的工具类，在其源代码中明显使用了将FileInputStream转变为Reader的方法。我们可以从这个类中得到一定的技巧。    

   $\color{YellowGreen}{ IO中的输出字符流 :}$

> Writer
>
> > BufferedWriter  
> > CharArrayWriter  
> > FilterWriter  
> > OutputStreamWriter  
> > PipedWriter  
> > PrintWriter  
> > StringWriter
> >
> > > FileWriter

1. Writer是所有的输出字符流的父类，它是一个抽象类。     
2. CharArrayWriter、StringWriter是两种基本的介质流，它们分别向Char数组、String中写入数据。PipedWriter是向与其它线程共用的管道中写入数据。   
3. BufferedWriter是一个装饰器为Writer提供缓冲功能。
4. PrintWriter和PrintStream极其类似，功能和使用也非常相似。
5. OutputStreamWriter是OutputStream到Writer转换的桥梁。

### 4. NIO代码实现:

服务端:

```text
package com.qingyi.server;

import java.io.IOException;
import java.net.InetSocketAddress;
import java.nio.ByteBuffer;
import java.nio.channels.SelectionKey;
import java.nio.channels.Selector;
import java.nio.channels.ServerSocketChannel;
import java.nio.channels.SocketChannel;
import java.util.Iterator;

public class NIOServer {
     //通道管理器
    private Selector selector;

    /**
    * 获得一个ServerSocket通道，并对该通道做一些初始化的工作
    * @param port  绑定的端口号
    * @throws IOException
    */
    public void initServer(int port) throws IOException {
         // 获得一个ServerSocket通道
         ServerSocketChannel serverChannel = ServerSocketChannel.open();
         // 设置通道为非阻塞
         serverChannel.configureBlocking(false);
         // 将该通道对应的ServerSocket绑定到port端口
         serverChannel.socket().bind(new InetSocketAddress(port));
         // 获得一个通道管理器
         this.selector = Selector.open();
         //将通道管理器和该通道绑定，并为该通道注册SelectionKey.OP_ACCEPT事件,注册该事件后，
         //当该事件到达时，selector.select()会返回，如果该事件没到达selector.select()会一直阻塞。
         serverChannel.register(selector, SelectionKey.OP_ACCEPT);
    }

    /**
    * 采用轮询的方式监听selector上是否有需要处理的事件，如果有，则进行处理
    * @throws IOException
    */
    @SuppressWarnings("unchecked")
    public void listen() throws IOException {
         System.out.println("服务端启动成功！");
         // 轮询访问selector
         while (true) {
              //当注册的事件到达时，方法返回；否则,该方法会一直阻塞
              selector.select();
              // 获得selector中选中的项的迭代器，选中的项为注册的事件
              Iterator ite = this.selector.selectedKeys().iterator();
              while (ite.hasNext()) {
                   SelectionKey key = (SelectionKey) ite.next();
                   // 删除已选的key,以防重复处理
                   ite.remove();
                   // 客户端请求连接事件
                   if (key.isAcceptable()) {
                        ServerSocketChannel server = (ServerSocketChannel) key
                                  .channel();
                        // 获得和客户端连接的通道
                        SocketChannel channel = server.accept();
                        // 设置成非阻塞
                        channel.configureBlocking(false);

                        //在这里可以给客户端发送信息哦
                        channel.write(ByteBuffer.wrap(new String("向客户端发送了一条信息").getBytes()));
                        //在和客户端连接成功之后，为了可以接收到客户端的信息，需要给通道设置读的权限。
                        channel.register(this.selector, SelectionKey.OP_READ);

                        // 获得了可读的事件
                   } else if (key.isReadable()) {
                             read(key);
                   }

              }

         }
    }
    /**
    * 处理读取客户端发来的信息 的事件
    * @param key
    * @throws IOException
    */
    public void read(SelectionKey key) throws IOException{
         // 服务器可读取消息:得到事件发生的Socket通道
         SocketChannel channel = (SocketChannel) key.channel();
         // 创建读取的缓冲区
         ByteBuffer buffer = ByteBuffer.allocate(100);
         channel.read(buffer);
         byte[] data = buffer.array();
         String msg = new String(data).trim();
         System.out.println("服务端收到信息："+msg);
         ByteBuffer outBuffer = ByteBuffer.wrap(msg.getBytes());
         channel.write(outBuffer);// 将消息回送给客户端
    }

    /**
    * 启动服务端测试
    * @throws IOException
    */
    public static void main(String[] args) throws IOException {
         NIOServer server = new NIOServer();
         server.initServer(8000);
         server.listen();
    }


}
```

消费端:

```text
package com.qingyi.client;

import java.io.IOException;
import java.net.InetSocketAddress;
import java.nio.ByteBuffer;
import java.nio.channels.SelectionKey;
import java.nio.channels.Selector;
import java.nio.channels.SocketChannel;
import java.util.Iterator;

public class NIOClient {
     //通道管理器
    private Selector selector;

    /**
    * 获得一个Socket通道，并对该通道做一些初始化的工作
    * @param ip 连接的服务器的ip
    * @param port  连接的服务器的端口号        
    * @throws IOException
    */
    public void initClient(String ip,int port) throws IOException {
         // 获得一个Socket通道
         SocketChannel channel = SocketChannel.open();
         // 设置通道为非阻塞
         channel.configureBlocking(false);
         // 获得一个通道管理器
         this.selector = Selector.open();

         // 客户端连接服务器,其实方法执行并没有实现连接，需要在listen（）方法中调
         //用channel.finishConnect();才能完成连接
         channel.connect(new InetSocketAddress(ip,port));
         //将通道管理器和该通道绑定，并为该通道注册SelectionKey.OP_CONNECT事件。
         channel.register(selector, SelectionKey.OP_CONNECT);
    }

    /**
    * 采用轮询的方式监听selector上是否有需要处理的事件，如果有，则进行处理
    * @throws IOException
    */
    @SuppressWarnings("unchecked")
    public void listen() throws IOException {
         // 轮询访问selector
         while (true) {
              selector.select();
              // 获得selector中选中的项的迭代器
              Iterator ite = this.selector.selectedKeys().iterator();
              while (ite.hasNext()) {
                   SelectionKey key = (SelectionKey) ite.next();
                   // 删除已选的key,以防重复处理
                   ite.remove();
                   // 连接事件发生
                   if (key.isConnectable()) {
                        SocketChannel channel = (SocketChannel) key
                                  .channel();
                        // 如果正在连接，则完成连接
                        if(channel.isConnectionPending()){
                             channel.finishConnect();

                        }
                        // 设置成非阻塞
                        channel.configureBlocking(false);

                        //在这里可以给服务端发送信息哦
                        channel.write(ByteBuffer.wrap(new String("向服务端发送了一条信息11111").getBytes()));
                        //在和服务端连接成功之后，为了可以接收到服务端的信息，需要给通道设置读的权限。
                        channel.register(this.selector, SelectionKey.OP_READ);

                        // 获得了可读的事件
                   } else if (key.isReadable()) {
                             read(key);
                   }

              }

         }
    }
    /**
    * 处理读取服务端发来的信息 的事件
    * @param key
    * @throws IOException
    */
    public void read(SelectionKey key) throws IOException{
        SocketChannel channel = (SocketChannel) key.channel();
        ByteBuffer buffer = ByteBuffer.allocate(100);
        channel.read(buffer);
        byte[] data = buffer.array();
        String msg = new String(data).trim();
        System.out.println("客户端收到回复信息："+msg);
    }


    /**
    * 启动客户端测试
    * @throws IOException
    */
    public static void main(String[] args) throws IOException {
         NIOClient client = new NIOClient();
         client.initClient("localhost",8000);
         client.listen();
    }

}
```

## 代办

* [ ] IO 源码阅读 \[\]

