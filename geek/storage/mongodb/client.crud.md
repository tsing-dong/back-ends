#### 基本数据类型：
```
字符串 - 这是用于存储数据的最常用的数据类型。MongoDB中的字符串必须为UTF-8。
整型 - 此类型用于存储数值。 整数可以是32位或64位，具体取决于服务器。
布尔类型 - 此类型用于存储布尔值(true / false)值。
双精度浮点数 - 此类型用于存储浮点值。
最小/最大键 - 此类型用于将值与最小和最大BSON元素进行比较。
数组 - 此类型用于将数组或列表或多个值存储到一个键中。
时间戳 - ctimestamp，当文档被修改或添加时，可以方便地进行录制。
对象 - 此数据类型用于嵌入式文档。
对象 - 此数据类型用于嵌入式文档。
Null - 此类型用于存储Null值。
符号 - 该数据类型与字符串相同; 但是，通常保留用于使用特定符号类型的语言。
日期 - 此数据类型用于以UNIX时间格式存储当前日期或时间。您可以通过创建日期对象并将日，月，年的日期进行指定自己需要的日期时间。
对象ID - 此数据类型用于存储文档的ID。
二进制数据 - 此数据类型用于存储二进制数据。
代码 - 此数据类型用于将JavaScript代码存储到文档中。
正则表达式 - 此数据类型用于存储正则表达式。

```

#### create database:
```
// 如果没有数据库就创建数据库，如果有直接返回数据库
use databaseName
```

#### use database:
```
// 查看当前使用的数据库
db

// 查看所有的数据库列表
show dbs
```

#### drop database:
```
use databaseName

db..dropDatabase();
```

#### 数据库管理：
```
    当数据库中还没有集合时，只有在执行 insert 时，才会检查数据库中有没有集合，如果没有集合就会创建集合，然后将新增的文档插入到集合中。还在磁盘上创建数据库。

    创建集合的时候，mongodb 会在磁盘上创建一系列的数据库文件集合，包括所有的集合，索引，还有其他的元数据。 如果去不同的机器中看到的创建的文件可能不一致。

    首先注意 mongod.lock 文件，它可以存储服务器的进程ID，不要删除或者修改锁的文件。

    所有的数据库文件前缀都应该有自己的数据库名称。（但是我的没有）。
    以 .ns 结尾的表明是命名空间。每个集合和索引的元数据有自己的命名空间文件。它的组织形式是哈希表。默认情况下 .ns 文件固定大小是 16m ,它允许存储 26000 个数据。但是要看单个文档的大小，总的来说它不会超过 26000 。

    mongodb 还会预分配数据文件，当有数据插入文档时会分配更多的数据文件，每个新的文件都是新生成的文件的 2 倍，直到文件达到 2g 的上限为止，后续的文件都是 2g。

    通过 db.stats() 可以查询
```


#### create collection:
```
// options 可选参数
db.createCollection(name, options)
```

#### drop collection:
```
db.lidong.drop()
```

#### 集合管理：
```
    基础的集合不用整理，主要整理一下特殊的集合。

    盖子集合：
        盖子集合是说集合的存储量是有上限的，当达到上限时最先进的数据就会废除掉。
    
    db.createCollection("gaizijihe", {capped:true, size:1000, max:2})

    执行插入 2000 行数据，等执行完成之后，查询数据，发现只有两条数据。只保留了最后的两条数据。

    TTL集合：
        当文档创建的时间超过当前时间，数据就会删除。
        
        db.dong.createIndex({time_field:1},{expireAfterSeconds:30})

        db.dong.insert({
        time_field:new Date(),
        name:"Jing"
        })
    

```

#### insert：
```
// 简单的插入数据
db.demo.insert(
    {"name": 'Do.L'}
)

// batch Insert
for(i=0; i<=2000;i++){
    db.numbers.save({uum:i})
}
```

#### delete or drop：
```
// 清空所有集合：
db.getCollection('demo').remove()

// 条件删除数据：
db.getCollection('demo').remove({
        "name":"Do.L"
})

// 删除集合：
db.getCollection('demo').drop()

// 删除单条数据用 remove
```

#### update:
```
// 使用 $set 操作符号进行文档修改
db.demo.update(
    {name:"Jar"},
    {   
        $set:{
            county:"中国"
        }
    }
)

// 不使用 $set 操作的话，是对整个文档的修改，将原有的文档进行删除并新增现在的字段。
db.demo.update(
    { name:"Do.L"},
    { county:"中国" }
)

// 使用 $unset 删除字段
db.demo.update(
    { name:"Do.L"},
    { $unset :
        {county:"国"} //这个字段的值可以不一致
    }
)

// 更新复杂的数据 设置
db.demo.update({ name:"Jar"},
    {   
        $set :{
            favorites:{
                citys:["杭州","南京"]
            }
        }
})


// 高级更新
db.getCollection('demo').update(
        { "favorites.citys":"杭州"},
        { $addToSet : {
                "favorites.citys":"丽江"
          }
        },
        false,
        true
)
false: 控制是否允许 updtate,当一个文档不存在时是否插入数据，这个是说明，是更新操作还是替换操作。

true: 是否多个更新，mongodb 默认只更新匹配到的第一个文档，如果想要更新所有的用户，这个必须是 true.
```

#### conditional Query:
```
// 简单的条件查询
db.demo.find(
   {
       name:"Jar"
    }
)

// 多条件查询，默认是 and 
db.demo.find(
   { 
       name:"Jar",
      _id:ObjectId("5e0077c308193deeacbea092")
   }
)

// 使用 $and 操作符号查询
db.demo.find(
    { 
        $and: [
            { name:"Jar"},
            {_id:ObjectId("5e0077c308193deeacbea092")}
        ]
    }
)

// 使用 $or 操作符号查询
db.demo.find(
    { 
        $or: [
            { name:"Jar"},
            { name:"Do.L"}
        ]
    }
)

// 范围查询 $gt 大于  $lt 小于 $gte 大于等于  $lte 小于等于 $ne 不等于 
db.getCollection('numbers').find({
        uum:{"$gt":1978} //大于
})

db.getCollection('numbers').find({
        uum:{"$lt":20} //小于
})

db.getCollection('numbers').find({
        uum:{"$lt":30,"$gt":20} //大于20 小于 30
})

// 多层查询 查询喜欢杭州的用户
db.getCollection('demo').find({
    "favorites.citys":"杭州"
})

// 分页查询 skip 是偏移量 limit 是每页显示的数量 sort 排序  -1 和 1 来规定排序的规则
db.getCollection('numbers').find({}).skip(10).limit(10).sort({'uum':1})


//模糊查询数据： 查询开头是 D 的数据
db.getCollection('dong').find({
        'name': /^D/
})

```

#### 投影查询:
```
db.getCollection('tree').find({},{name:1})
```

