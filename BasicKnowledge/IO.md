# IO 基础编程:
## 1. 简介:   
&emsp;&emsp;IO 分为两类: java.io中阻塞流和java.nio中非阻塞流。   
&emsp;&emsp;&emsp;$\color{YellowGreen}{阻塞流}$：面向流操作的。   
&emsp;&emsp;&emsp;&emsp;从流中读取数一个字节或者多个字节，直至读完所有的字节，没有任何缓存的地方。还不能移动流中的数据，如果想要操作数据，需要将数据写入到缓存中进行处理。      
&emsp;&emsp;&emsp;&emsp; java io 的各种流的操作都是阻塞的, 当在线程调用 read()或者writer()时,该线程被阻塞,直到数据完全操作完成才能操作其他的事情。     
&emsp;&emsp;&emsp;$\color{YellowGreen}{非阻塞流}$:  面向缓冲区。將数据直接放入缓存中,可以直接操作数据,但是在操作数据之前,需要查看缓存中是否有需要处理的数据。而且在处理数据时需要注意的是不能将没处理的数据处理了。      
&emsp;&emsp;&emsp;&emsp; java io 非阻塞模式,式一个线程从某个通道发起请求时,只能操作当前缓存中的数据,如果没有数据处理,就什么也不会操作,所以当数据还没处理完成之前可以操作缓存中的数据,当一个线程写入数据时,不需要等他全部写入就可以操作数据了。

TODO: NIO 选择器概念?

## 2. 处理数据: 
&emsp;&emsp; 如果纯粹的使用 nio 设计相较于 io 设计,数据处理方面比较麻烦:     
&emsp;&emsp; $\color{YellowGreen}{java-io :}$ 
```
Name: Anna 
Age: 25
Email: anna@mailserver.com 
Phone: 1234567890 
```
&emsp;&emsp; 处理过程:
```
InputStream input = ... ; // get the InputStream from the client socket   

BufferedReader reader = new BufferedReader(new InputStreamReader(input));   

String nameLine   = reader.readLine(); 
String ageLine    = reader.readLine(); 
String emailLine  = reader.readLine(); 
String phoneLine  = reader.readLine(); 
```
当执行完nameLine  readLine() 方法时,你会知道一行数据被处理完了,因为 readLine() 会一直阻塞,直到数据被处理完成。一旦数据被处理完成，就不能再次进行处理。

&emsp;&emsp; $\color{YellowGreen}{java-nio:}$  
```
ByteBuffer buffer = ByteBuffer.allocate(48); 
int bytesRead = inChannel.read(buffer); 
```
当执行  read(buffer) 时,你不知道需要处理的数据是否已经进入缓存中,比如: 当数据存到缓存中是 Name: An   这个时候对数据操作是没有意义的,这个时候就会去缓存中查看数据是否已经完整的存到缓存中。这样的操作使程序的设计异常的复杂。

## 3. 明细: 
&emsp;&emsp; $\color{YellowGreen}{IO中输入字符流:}$  
>Reader
>>CharArrayReader  
>>FilterReader   
>>PushbackReader     
>>InputStreamReader      
>>FileReader  
>>PipedReader       
>>StringReader   
>>BufferedReader
>>>LineNumberReader   

1. Reader是所有的输入字符流的父类，它是一个抽象类。   
2. CharReader、StringReader是两种基本的介质流，它们分别将Char数组、String中读取数据。PipedReader是从与其它线程共用的管道中读取数据。   
3. BufferedReader很明显就是一个装饰器，它和其子类负责装饰其它Reader对象。   
4. FilterReader是所有自定义具体装饰流的父类，其子类PushbackReader对Reader对象进行装饰，会增加一个行号。     
5.   InputStreamReader是一个连接字节流和字符流的桥梁，它将字节流转变为字符流。FileReader可以说是一个达到此功能、常用的工具类，在其源代码中明显使用了将FileInputStream转变为Reader的方法。我们可以从这个类中得到一定的技巧。    

&emsp;&emsp; $\color{YellowGreen}{ IO中的输出字符流 :}$ 
>Writer
>>BufferedWriter  
>>CharArrayWriter   
>>FilterWriter     
>>OutputStreamWriter      
>>PipedWriter  
>>PrintWriter       
>>StringWriter   
>>>FileWriter         

1. Writer是所有的输出字符流的父类，它是一个抽象类。     
2. CharArrayWriter、StringWriter是两种基本的介质流，它们分别向Char数组、String中写入数据。PipedWriter是向与其它线程共用的管道中写入数据。   
3. BufferedWriter是一个装饰器为Writer提供缓冲功能。
4. PrintWriter和PrintStream极其类似，功能和使用也非常相似。
5. OutputStreamWriter是OutputStream到Writer转换的桥梁。
   






# 代办
- [ ] IO 源码阅读 []
