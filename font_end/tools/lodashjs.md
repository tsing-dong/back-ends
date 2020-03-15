# lodashjs

## lodashjs 实践

## 官网地址： [https://www.lodashjs.com/](https://www.lodashjs.com/)

### array-数组 :

* \_.chunk\(array, \[size=1\]\):
  * 定义：
    * 将指定的数组按照指定的长度切割，当集合无法被分割全部相等长度的集合时，将剩余的数据存放到最后一个块中。
  * 案例：

    ```text
      // arr : _.chunk(array, [size=1]);
      const arr = [1, 3, 45, 6, 77, 8, 89];
      const result = _.chunk(arr, 2);
      console.log(result);
    ```

  * 结果：

    ```text
       [ [ 1, 3 ], [ 45, 6 ], [ 77, 8 ], [ 89 ] ]
    ```
* \_.compact\(array\):
  * 定义：
    * 将所有的 false, null, 0, "", undefined, 和 NaN 假数据。
  * 案例：

    ```text
      // _.compact(array);
      const arr = [0, 1, false, 2, '', 3, null, undefined];
      const result = _.compact(arr);
      console.log(result);
    ```

  * 结果：

    ```text
      [ 1, 2, 3 ]
    ```
* \_.concat\(array, \[values\]\):
  * 定义：
    * 拼接数组
  * 案例：

    ```text
      // _.concat(array, [values]);
      const arr = [23];
      const arr1 = [23, 423, 42424, 24323];
      const result = _.concat(arr, arr1);
      console.log(result);
    ```

  * 结果：

    ```text
      [ 23, 23, 423, 42424, 24323 ]
    ```
* \_.difference\(array, \[values\]\):
  * 定义：
    * 传入两个数组，array 是要检查的数组，\[values\] 是需要在检查的数组的排除的数据。
  * 案例：

    ```text
      const arr1 = [23, 423, 42424, 24323];
      const arr = [23];
      const result = _.difference(arr1, arr);
      console.log(result);
    ```

  * 结果：

    ```text
      [ 423, 42424, 24323 ]
    ```
* _.differenceBy\(array, \[values\], \[iteratee=_.identity\]\):
  * 定义：
    * 传一个函数进来，根据函数进行运算的结果再进行过滤数据。
  * 案例：

    ```text
      const arr1 = [3.1, 2.2, 1.3];
      const arr = [4.4, 2.5];
      const result = _.differenceBy(arr1, arr, Math.floor);
      console.log(result);
    ```

  * 结果：

    ```text
      [ 3.1, 1.3 ]
    ```
* \_.differenceWith\(array, \[values\], \[comparator\]\):
  * 定义：
    * 和上一个差不多，就是对数据处理。
  * 案例：

    ```text
      var objects = [{ 'x': 1, 'y': 2 }, { 'x': 2, 'y': 1 }];
      _.differenceWith(objects, [{ 'x': 1, 'y': 2 }], _.isEqual);
    ```

  * 结果：

    ```text
       [{ 'x': 2, 'y': 1 }]
    ```
* \_.drop\(array, \[n=1\]\):
  * 定义：
    * 切除数组前面 n 个元素
  * 案例：

    ```text
      const arr1 = [3, 2, 1];
      const result = _.drop(arr1, 2);
      console.log(result);
    ```

  * 结果：

    ```text
      [ 1 ]
    ```
* \_.dropRight\(array, \[n=1\]\):
  * 定义：
    * 去除 arr 尾部的的 n 个元素。
  * 案例：

    ```text
      const arr1 = [3, 2, 1];
      const result = _.dropRight(arr1, 2);
      console.log(result);
    ```

  * 结果：

    ```text
      [ 3 ]
    ```

// TODO: 这个在考虑一下

* _.dropRightWhile\(array, \[predicate=_.identity\]\):
  * 定义：
  * 案例：

// TODO: 这个在考虑一下

* _.dropWhile\(array, \[predicate=_.identity\]\)：
* \_.fill\(array, value, \[start=0\], \[end=array.length\]\)：
  * 定义：
    * 替换集合中的数据，可以设置从开始位置-结束位置替换数据。
  * 案例：

    ```text
      const arr1 = [3, 2, 1];
      //这个是开始位置到结束位置替换数据
      const result = _.fill(arr1, 'dong', 0, 1);
      //初始化数组的个数，初始化值。
      const m = _.fill(Array(3), 2);

      const arr2 = [3, 2, 1];
      // 替换所有的值
      const result1 = _.fill(arr2, 'dong');
      console.log(result1);
      console.log(m);
      console.log(result);
    ```
* _.findIndex\(array, \[predicate=_.identity\], \[fromIndex=0\]\)：
  * 定义：
    * 查找数组中元素的索引位置。
  * 案例：

    ```text
      const arr1 = [3, 2, 1];
      //这个是开始位置到结束位置替换数据
      const result = _.findIndex(arr1, function (o) {
          return o === 2;
      });
      console.log(result);
    ```

  * 结果：

    ```text
      1
    ```
* _.findLastIndex\(array, \[predicate=_.identity\], \[fromIndex=array.length-1\]\):
  * 定义：
    * 和上面一个差不多，但是她是从右向左查找的第一个索引的位置。
  * 案例：

    ```text
      const arr1 = [3, 2, 1, 3, 6];
      //这个是开始位置到结束位置替换数据
      const result = _.findLastIndex(arr1, function (o) {
          return o === 3;
      });
      console.log(result);
    ```

  * 结果：

    ```text
      3
    ```
* \_.flatten\(array\):
  * 定义：
    * 减少嵌套的层次。集合中的是对象的化还待验证。
  * 案例：

    ```text
      const arr1 = [3, [12, 23, 23]];
      const result = _.flatten(arr1);
      console.log(result);
    ```

  * 结果：

    ```text
      [ 3, 12, 23, 23 ]
    ```
* \_.flattenDepth\(array, \[depth=1\]\):
  * 定义：
    * 减少嵌套深度，可以选择减少嵌套的几层。
  * 案例：

    ```text
      const arr1 = [1, [22, 22, 22, [33, 33, 33]]];
      const result = _.flattenDepth(arr1, 2);
      console.log(result);

      const arr2 = [{ "age": 1 }, [{ "age": 22 }, { "age": 22 }, { "age": 22 }, [{ "age": 33 }, { "age": 33 }, { "age": 33 }]]];
      const result1 = _.flattenDepth(arr2, 2);
      console.log(result1);
    ```

  * 结果：

    ```text
      [ 1, 22, 22, 22, 33, 33, 33 ]
      [ { age: 1 },
      { age: 22 },
      { age: 22 },
      { age: 22 },
      { age: 33 },
      { age: 33 },
      { age: 33 } ]
    ```

// TODO: 这个待研究场景

* \_.fromPairs\(pairs\):
* \_.head\(array\)：
  * 定义：
    * 获取元素的第一个元素。
  * 案例：

    ```text
      const arr1 = [2, 22, 22, 22, 1];
      const result = _.head(arr1);
      console.log(result);
    ```

  * 结果：

    ```text
      2
    ```
* \_.indexOf\(array, value, \[fromIndex=0\]\):

