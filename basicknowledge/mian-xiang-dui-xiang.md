# 面向对象

## 继承 :

  1. 什么是继承?  
     多个类中存在相同的属性和行为时,将这些相同的内容抽取到单独的一个类中,其他的类无需定义相同的属性,只要继承那个类即可。  
     多个类可以成为子类，单独的类称为父类，超类，或者基类。  
     子类可以直接访问父类中非私有的属性和行为。

  2. 实现继承的方式?  
    通过  extends 关键字让类和类之间产生关系。  
    案例：

```text
     class SubDemo extends Demo{}    //SubDemo是子类，Demo是父类
```

  3. 继承的好处?  
     提高代码的复用性  
     让类和类之间产生了关系,是多态的前提

  4. 继承的特点?  
     java 只支持单继承,不支持多继承。

```text
        //一个类只能有一个父类，不可以有多个父类。
        class SubDemo extends Demo{} //ok
        lass SubDemo extends Demo1,Demo2...//error
```

     java 支持多重继承

```text
        class A{}
        class B extends A{}
        class C extends B{}
```

## 多态 :

  1. 什么是多态?  
     对象在不同时刻表现出现的不同状态。

  2. 多态的前提?  
     要有继承或者实现关系。  
     要有方法的重写。  
     要有父类引用指向子类对象。

  3. 程序中概念?  
     父类或者接口的引入指向或者接受自己的子类对象。

  4. 好处和坏处?  
     多态的存在提高了程序的扩展性和后期可维护性。  
     父类调用的时候只能调用父类里的方法，不能调用子类的特有方法，因为你并不清楚将来会有什么样的子类继承你。

  5. 多态时成员的特点?  
     &gt; 成员变量:  
      编译时期：看引用型变量所属的类中是否有所调用的变量；  
      运行时期：也是看引用型变量所属的类是否有调用的变量。  
      成员变量无论编译还是运行都看引用型变量所属的类，简单记成员变量，编译和运行都看等号左边。

     &gt; 成员方法：  
       编译时期：要查看引用变量所属的类中是否有所调用的成员；  
       运行时期：要查看对象所属的类中是否有所调用的成员。如果父子出现同名的方法,会运行子类中的方法,因为方法有覆盖的特性。  
       编译看左边运行看右边。

     &gt; 静态方法:  
       编译时期：看的引用型变量所属的类中是否有所调用的变量；  
       运行时期：也是看引用型变量所属的类是否有调用的变量。  
       编译和运行都看等号左边。

  6. 注意事項?  
       一定不能够将父类的对象转换成子类类型！  
       父类的引用指向子类对象，该引用可以被提升，也可以被强制转换。  
       多态自始至终都是子类对象在变化

案例：

```text
        //多态向下转型和向上转型的例子，多态转型解决了多态中父类引用不能使用子类特有成员的弊端。
class PolymorphicTest2 {
    public static void main(String[] args) {
        Phone p1 = new Nokia();        //向上转型，类型提升
        Nokia no = (Nokia)p1;          //向下转型，强制将父类的引用转换成子类类型，不能将Nokia类型转成Moto或Nexus类型
        no.print();                    //输出结果为Phone---null---0，因为继承了父类的方法

        Phone p2 = new Moto();
        Moto m = (Moto)p2;
        m.print();                    //输出结果为Moto---yellow---1599，方法重写，子类方法覆盖父类方法

        Phone p3 = new Nexus();
        Nexus ne = (Nexus)p3;
        ne.print();
    }
}

class Phone{    
    String color;
    int price;

    public void print(){
        System.out.println("Phone---" + color + "---" + price );
    }    
}

class Nokia extends Phone{
    String color = "red";
    int price = 1009;

    //public void print(){
    //    System.out.println("Nokia---" + color + "---" + price);
    //}
}

class Moto extends Phone{
    String color = "yellow";
    int price = 1599;

    public void print(){
        System.out.println("Moto---" + color + "---" + price);
    }
}

class Nexus extends Phone{
    String color = "black";
    int price = 1999;

    public void print(){
        System.out.println("Nexus---" + color + "---" + price);
    }
}
}
```

## 封装:

  1. 什么是封裝?  
     &gt; 封装是隐藏实现细节,使用者通过接口使用数据。使用 private，protected和public实现封装。  
     &gt; 封装可以隐藏实现的细节。  
     &gt; 让使用者只能通过实现写好的访问方法来访问这些字段，这样一来我们只需要在这些方法中增加逻辑控制，限制对数据的不合理访问。  
     &gt; 方便数据检查，有利于于保护对象信息的完整性。  
     &gt; 便于修改，提高代码的可维护性。

  2. 注意事项?  
     &gt; 把字段（成员变量）和实现细节隐藏起来，不允许外部直接访问。  
     &gt; 把方法暴露出来，让方法控制这些成员变量进行安全的访问和操作。

