# 循环

## 循环简介:

   Java 中基本的循环结构:  
     while 循环  
     do…while 循环  
     for 循环

## while 循环:

案例:

```text
public class Test {
   public static void main(String args[]) {
      int x = 10;
      while( x < 20 ) {
         System.out.print("value of x : " + x );
         x++;
         System.out.print("\n");
      }
   }
}
```

## do…while 循环:

说明:    do…while 至少循环一次

案例:

```text
public class Test {
   public static void main(String args[]){
      int x = 10;

      do{
         System.out.print("value of x : " + x );
         x++;
         System.out.print("\n");
      }while( x < 20 );
   }
}
```

## for循环:

案例:

```text
public class Test {
   public static void main(String args[]) {

      for(int x = 10; x < 20; x = x+1) {
         System.out.print("value of x : " + x );
         System.out.print("\n");
      }
   }
}
```

## Java 增强 for 循环:

说明:    增强 for 是在 jdk1.5之后出来的。 案例:

```text
for(声明语句 : 表达式)
{
   //代码句子
}
```

## break 关键字:

说明:  
   break 主要用在循环语句或者 switch 语句中，用来跳出整个语句块。 break 跳出最里层的循环，并且继续执行该循环下面的语句。

## continue 关键字:

说明:  
   跳过本次循环。

