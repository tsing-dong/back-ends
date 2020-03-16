# Promise对象

### Promise的含义:
- Promise 是一种异步编程的解决方案，和传统的纯回调函数和事件相比会更加强大和合理。es6中写入语言标准，统一用法。
- Promise 对象的特点：
    - a. 对象的状态不受外部的影响。Promise 对象代表一个异步的操作，任何操作都没有办法改变状态。有三种状态：
        - pending(进行中)
        - fulfilled(已成功)
        - rejected(已失败)
    - b. 一旦状态改变，就不会在变，任何时候都可以得到这个结果。Promise 对象的状态改变只有两种可能：
        - 从 pending -> fulfilled 
        - 从 pending -> rejected  
    只要这两种状态发生，状态就固定了，不会在变，会一直保持这个结果，这时就称为resolved(已定型)。

---

### 基本的用法
- 定义：
    - es6 规定，Promise 对象是一个构造函数，用来生成 Promise 实例。
    - 案例：
        ```js
            const promise = new Promise(function (resolve, reject){
                // code

                if (/*异步操作成功*/) {
                    resolve ( value )
                } else {
                    reject ( value )
                }
            });
        ```
    - 解释：
        - Premoise 构造函数接受一个函数作为参数，该函数的两个参数分别是 resolve 和 reject。他们是两个函数，由 javaScript 引擎提供，不用自己部署。
        - resolve 函数：
            - 将 Promise 对象的状态从 “未完成” 变成 “成功”，在异步操作成功时调用，并将异步操作的结果，作为参数传递出去；
        - reject 函数：
            - 将 Promise 对象的状态从 “未完成” 变成 “失败”，在异步操作失败时调用，并将异步操作的结果，作为参数传递出去；
    - Promise 实例生成以后，可以用 then 方法分别指定 resloved 和 rejected 状态的回调函数。
        ```js
            promise.then(
                function(value){
                //成功
                },
                function(error){
                //失败
                },
            );

        ```
    - 解释：
        - then 方法可以接受两个回调函数作为参数。
            - 第一个回调函数是 Promise 对象的状态变为 resolved 时调用；
            - 第二个回调函数是 Promise 对象的状态变为 rejected 时调用；
            - 其中，第二个函数是可选的，并不一定要提供。
    - 案例 1：
        ```js
            function timeout(ms) {
                return new Promise((resolve, reject) => {
                    setTimeout(resolve, ms, 'done');
                });
            }

            timeout(100).then((value) => {
                console.log(value);
            });
        ```
    - 案例 2：
        ```js
            // Promise 新建之后会立即执行
            let promise = new Promise(function(resolve, reject) {
                console.log('Promise');
            resolve();
            });

            promise.then(function() {
                console.log('resolved.');
            });

            console.log('Hi!');

            // Promise
            // Hi!
            // resolved
        ```
    - 案例 3：
        ```js
            // Promise resolve 或者 rejected 并不会终结 Promise 的函数执行
            let promise = new Promise(function(resolve, reject) {
                console.log('Promise');
                resolve();
            });

            promise.then(function() {
                console.log('resolved.');
            });

            console.log('Hi!');

            // Promise
            // Hi!
            // resolved

            //一般来说，调用resolve或者reject以后，Promise 的使命就完成了，后续的操作应该放在 then 方法里面，而不应该写在 resolve 或者 reject 的后面。所以，最好在他们前面加上 return 语句，这样就不会出现意外。

            new Promise ((resolve, reject) => {
                rerturn resolve(1);
                //后面的语句不会执行
                console.log(2);
            });
        ```

### Promise.prototype.then()

### Promise.prototype.catch()

### Promise.prototype.finally()

### Promise.all()

### Promise.race()

### Promise.allSettled()

### Promise.any()

### Promise.resolve()

### Promise.reject()

