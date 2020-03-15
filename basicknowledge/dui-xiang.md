# Java 对象和类:

   1. java 作为一种面向对象语言,支持以下基本概念:  
     多态,继承,封装,抽象,类,对象,实例,方法,重载.  
   2. 对象和类的概念:  
     对象和类的概念:  
       对象:  
         对象是一个类的实例,有状态有行为.  
       类:  
         类是一个对象的模板,用来描述行为和状态.  
   3. java 中的类:  
     类中的变量:  
       局部变量:  
         在方法、构造方法或者语句块中定义的变量被称为局部变量。变量声明和初始化都是在方法中，方法结束后，变量就会自动销毁。  
       成员变量：  
         成员变量是定义在类中，方法体之外的变量。这种变量在创建对象的时候实例化。成员变量可以被类中方法、构造方法和特定类的语句块访问。        类变量：  
         类变量也声明在类中，方法体之外，但必须声明为static类型。

   4. java 构造方法:  
     每个类中都有构造方法,如果没有显示的给构造方法,java编译器将会提供一个默认的构造方法。 构造方法和类名相同，一个类中可以有多个构造方法。

   5. java 创建对象:  
     声明:  
         声明一个对象，包括对象名称和对象类型。  
     实例化:  
         使用 new 关键字创建对象。  
     初始化:  
         使用 new 关键字创建对象时，会调用构造方法来初始化对象。

案例：

```text
public class Puppy{
   public Puppy(String name){
      //这个构造器仅有一个参数：name
      System.out.println("小狗的名字是 : " + name ); 
   }
   public static void main(String[] args){
      // 下面的语句将创建一个Puppy对象
      Puppy myPuppy = new Puppy( "tommy" );
   }
}

运行结果:
小狗的名字是 : tommy
```

   6. java 访问实例变量和方法:  
案例:

```text
/* 实例化对象 */
Object referenceVariable = new Constructor();
/* 访问类中的变量 就是类中方法外的变量*/
referenceVariable.variableName;
/* 访问类中的方法 */
referenceVariable.methodName();


public class Puppy{
   int puppyAge;
   public Puppy(String name){
      // 这个构造器仅有一个参数：name
      System.out.println("小狗的名字是 : " + name ); 
   }

   public void setAge( int age ){
       puppyAge = age;
   }

   public int getAge( ){
       System.out.println("小狗的年龄为 : " + puppyAge ); 
       return puppyAge;
   }

   public static void main(String[] args){
      /* 创建对象 */
      Puppy myPuppy = new Puppy( "tommy" );
      /* 通过方法来设定age */
      myPuppy.setAge( 2 );
      /* 调用另一个方法获取age */
      myPuppy.getAge( );
      /*你也可以像下面这样访问成员变量 */
      System.out.println("变量值 : " + myPuppy.puppyAge ); 
   }
}

结果:
小狗的名字是 : tommy
小狗的年龄为 : 2
变量值 : 2
```

