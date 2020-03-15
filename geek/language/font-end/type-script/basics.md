# 基本数据类型

## 1. boolean

* 注意：
  * 1. 使用构造函数 Boolean 创造的对象不是布尔值， 返回的是对象。
       * let createdByNewBoolean: boolean = new Boolean\(1\);
  * 1. 直接调用 Boolean 也可以返回一个 boolean 类型。
       * let createdByBoolean: boolean = Boolean\(1\);
* 案例：

  ```javascript
    let isBoolean: boolean = false;
    console.log(isBoolean);
  ```

## 2. number

* 注意：
  * null
* 案例：

  ```javascript
    let isNumber: number = 1;
    console.log("numberis" + isNumber);
  ```

## 3. string

* 注意：
  * null
* 案例：

  ```javascript
    let isString = 'Do';
    let appendNumber = 23;
    let personDesc: string = `Hello, my name is ${isString} , age is ${appendNumber}`;
    console.log(personDesc);
  ```

## 4. null,undefined

* 注意：
  * 1. TypeScript 没有空值（Void）的概念，在 TypeScript 中，可以用 void 表示没有任何返回值的函数。
  * 1. 变量声明了，还没赋值 = undefined
* 案例：

  ```javascript
    function isNull(): void {
        alert('My name is Do.');
    }
    const isNullResult = this.isNull();
    console.log(isNullResult); // 返回的 undefined
  ```

## 5. any

* 注意：
  * 1. 如果是一个任意值，在赋值过程中改变类型。
* 案例：

  ```javascript
    let ageNumber: number = 23;
    ageNumber = '34'; //这个是不能被赋值的。
    console.log(ageNumber);
    //如果是 any 类型，则允许被修改。
    let nameString: any = 'Do.';
    nameString = 34;
    console.log(nameString);
  ```

## 6. attribute & method is any

* 注意：
  * 1. 在任意值上访问的任何属性都是被允许的。
  * 1. 也可以调用任何方法。
* 案例：

  \`\`\`js

    let personAny: any = 'Do.';

    console.log\(personAny.person.name\); // 运行报错

    let personAny: any = {

  ```text
    "name": 'Do.'
  ```

    };

    personAny.age = '34';

    personAny.childe.name = 'huanglei'; // 运行报错

    console.log\(personAny\);

```text
#### 7. 未声明类型的变量 
- 注意：
    - 1. 变量如果在声明的时候未指定具体类型，会被识别为任意类型。
- 案例：
```js
```

## 8. 类推类型

* 注意：
  * 1. TypeScript 在编译期间会给没有指定类型，但是 TypeScript 会默认的给一个类型。
* 案例：

  ```javascript

  ```

## 9. 联合类型

* 注意：
  * 1. 可以区值多种类型中的一种。
* 案例：

  ```javascript

  ```

## 10. 对象类型-接口

* 注意：
  * 1. 在面向对象的语言中，接口 （Interfaces） 很重要，具体的如何行动由实现类操作。
* 案例：

  ```javascript
    interface Person {
        readonly name: string; //只读属性
        [propName: string]: any; //任意属性
        age?: number; // 可选属性

    };

    let jar: Person = {
        name: "Do",
        age: 5
    };

    // 不能缺少属性
    let dong: Person = {
        name: "Do",
    };

    // 不能增加属性
    let dong: Person = {
        name: "Do",
        age: 5，
        sex: '男'，
    };

    // 可选属性
    let dong: Person = {
        name: "Do",
        age: 34,
        sex: '男'
    };
    // dong.name = 'jar';  这个不允许修改
    console.log(dong);
  ```

## 11. 数组类型

* 注意：
  * 1. 确认类型的数组中是不能有其他类型的。
* 案例：

  ```javascript
    // 基础：
    let arr: number[] = [1, 3, 345, 3]; 
    // 数组泛型
    let paradigmArr: Array<number> = [1, 1, 23, 342];
    paradigmArr.push('sd'); // 编译报错
    //any 数组类型：
    let list: any[] = ['23', 34];
  ```

## 12. 函数类型

* 注意：
  * null
* 案例：

  ```javascript
    // 声明函数
    function sum(x, y) {
        return x + y;
    }
    // 声明入参和出参的类型
    function sum(x:number, y:number):number {
        return x + y;
    }
    // 可选的参数
    function sum(x:number, y:number, lastName?:string):number {
        return x + y + lastName;
    }
    // 默认值
    function sum(x:number, y:number, lastName?:string = 'Do'):number {
        return x + y + lastName;
    }
    // 重载
    function reverse(x: number | string): number | string {
        if (typeof x === 'number') {
            return Number(x.toString().split('').reverse().join(''));
        } else if (typeof x === 'string') {
            return x.split('').reverse().join('');
        }
    }
    // 函数表达式
    let issum = function (x, y) {
        return x + y;
    }
    console.log(sum(23, 343));
    console.log(issum(1, 2));
  ```

## 13. 类型断言

* 注意：
  * 断言不是类型的转换，是判断是否是一种指定的类型。
* 案例：

  \`\`\`js

  function getLength\(something: string \| number\): number { if \(\(something\).length\) { return \(something\).length; } else { return something.toString\(\).length; } }

  console.log\(getLength\('23'\)\); console.log\(getLength\(23\)\);

\`\`\`

## 14. 声明文件

```text
TODO： 这个需要在实际的场景中应用再进行补充。
```

## 15. 内置对象

```text
TODO： 这个需要在实际的场景中应用再进行补充。
```

