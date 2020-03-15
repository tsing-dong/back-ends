# 异常

## Java 异常架构

![avatar](../.gitbook/assets/java-yi-chang-jia-gou.png)

## 一. 详细说明 :

### 1. Throwable :

   1.1 Throwable 是 Java 语言所有的错误或异常的超类。  
   1.2 Throwable 又分为两个子类 : Error 和 Exception , 他们通常用于指示发生了异常情况。  
   1.3 Throwable 包含了其线程创建时线程执行堆栈的快照，他提供了 printStackTrace（） 等接口用于获取堆栈跟踪数据等信息。

### 2. Exception :

   Exception 以及其子类是 Throwable 的一种形式。他指出了合理的应用程序想要捕获的条件。

### 3. RuntimeException  :

   RuntimeException 是那些可能 Java 虚拟机正常运行期间抛出的异常的超类。  
   编译器不会检查 RuntimeException 异常。

### 4. Error  :

   和 Exception 一样， Error 也是 Throwable 的子类。它用于指示合理的应用程序不应该试图捕获的严重问题，大多数这样的错误都是异常条件。  
   和RuntimeException一样，编译器也不会检查Error。

## 二. 3种抛出异常类型 :

   Java将可抛出\(Throwable\)的结构分为三种类型：  
    被检查的异常\(Checked Exception\)  
    运行时异常\(RuntimeException\)  
    错误\(Error\)。

### 1. 运行时异常  :

     定义 :  
      RuntimeException及其子类都被称为运行时异常。  
     特点 :  
       java 编译器不会检查他,编译器会通过,如果在运行时出现的错误,就称为运行时异常。

### 2. 被检查异常  :

     定义 :  
      Exception类本身，以及Exception的子类中除了"运行时异常"之外的其它子类都属于被检查异常。  
     特点 :  
       Java编译器会检查它。此类异常，要么通过throws进行声明抛出，要么通过try-catch进行捕获处理，否则不能通过编译。  
       例如，CloneNotSupportedException就属于被检查异常。当通过clone\(\)接口去克隆一个对象，而该对象对应的类没有实现Cloneable接口，就会抛出CloneNotSupportedException异常。  
       被检查异常通常都是可以恢复的。

### 3. 错误  :

     定义 :  
      Error类及其子类。  
     特点 :  
       和运行时异常一样，编译器也不会对错误进行检查。  
       当资源不足、约束失败、或是其它程序无法继续运行的条件发生时，就产生错误。程序本身无法修复这些错误的。例如，VirtualMachineError就属于错误。  
       按照Java惯例，我们是不应该是实现任何新的Error子类的！

