#### 1. 类型别名 
- 注意：
    - 这个还是有点模糊
- 案例：
```js
    type Name = number;
    type NameResolver = () => number;
    type NameOrResolver = Name | NameResolver;
    function getName(n: NameOrResolver): Name {
        if (typeof n === 'number') {
            return n;
        } else {
            return n();
        }
    }
    // console.log(getName('43'));
    console.log(getName(4));
```

#### 2. 字符串字面常量
- 注意：
    - 只能获取定义的值。
- 案例：
```js
    type eventName = 'beijing' | 'nanjing' | 'tianjing';
    function getType(type: eventName) {
        return type;
    }
    console.log(getType('nanjing')); 
```

#### 3. 元组
- 注意：
    - 数组合并相同的对象，元组合并不同得对象。
    - 如果在声明元组时就直接赋值，需要将所有的值都初始化。
    - 数组是不能越界的。
- 案例：
```js
    type eventName = 'beijing' | 'nanjing' | 'tianjing';
    function getType(type: eventName) {
        return type;
    }
    console.log(getType('nanjing')); 
```

#### 4. 枚举
- 注意：
    - null
- 案例：
```js
    enum Days { Sun, Mon, Tuw, Wed, Thu, Fri, Sat };
    console.log(Days["Sun"] === 0); // true
    console.log(Days["Mon"] === 1); // true
    console.log(Days["Tue"] === 2); // true
    console.log(Days["Sat"] === 6); // true

    console.log(Days[0] === "Sun"); // true
    console.log(Days[1] === "Mon"); // true
    console.log(Days[2] === "Tue"); // true
    console.log(Days[6] === "Sat"); // true
```

#### 5. 类
- 注意：
    - 1. 使用 private 修饰的属性和方法，在子类中是不允许访问的。
    - 2. 使用 protected 修饰的属性和方法在子类中可以访问。
- 案例：
```js
   class People {

        public name;
        private age;
        protected sex;
        constructor(name, age) {
            this.name = name;
            this.age = age;
        }
        sayHello() {
            return `Hotel name is ${this.name} age is ${this.age}`;
        }
    }

    let a = new People('丽江客栈', 34);
    console.log(a.sayHello()); // 这个时候 age 是可以访问的，但是不能赋值。

    //抽象类
    abstract class Animal {
        public name;
        public constructor(name) {
            this.name = name;
        }
        public abstract sayHi();
    }

    class Dog extends Animal {
        public eat() {
            console.log(this.name);
        }
        //子类必须实现父亲的抽象方法
        public sayHi() {
            console.log('父亲的方法');
        }
    }

    let dog = new Dog('test');
    console.log(dog.sayHi());
    console.log(dog.eat());
```

#### 6. 类和接口
- 注意：
    - 1. 一个类可以实现多个接口。
    - 2. 接口继承类。
    - 3. 接口继承接口。
- 案例：
```js
    interface Alarm {
    alert();
    }

    class Door {

    }

    class SecuriytDoor extends Door implements Alarm {
        alert() {
            console.log('extends Door implements Alarm');
        }
    }
```

#### 7. 泛型
- 注意：
    - null
- 案例：
```js
    function createArray<T>(length: number, value: T): Array<T> {
    let result: T[] = [];
    for (let i = 0; i < length; i++) {
        result[i] = value;
    }
    return result;
    }

    createArray<string>(3, 'x'); 
```

#### 7. 声明合并
- 注意：
    - 1.接口合并，如果两个接口名称相同，就会将接口中的属性和方法合并成一个，在合并的过程中如果名称一致没问题，但是如果名称一致但是类型不一致就会报错。
- 案例：
```js
    function reverse(x: number): number;
    function reverse(x: string): string;
    function reverse(x: number | string): number | string {
        if (typeof x === 'number') {
            return Number(x.toString().split('').reverse().join(''));
        } else if (typeof x === 'string') {
            return x.split('').reverse().join('');
        }
    }
```