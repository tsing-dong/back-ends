#### 聚合：
```
    聚合管道：
        一个操作的输出作为下一个操作的输入。
    聚合管道操作包含下面的部分：
        $project:
            指定输出文档里字段。(从集合中选择出特定的字段)
        $match:
            选择要处理的文档，和find相似。
        $limit:
            限制传递给下一步的文档数量。
        $skip:
            跳过一定数量的文档。
        $unwind:
            扩展数组，为每一个数组入口生成一个输出文档。
        $group:
            根据 key 来分组文档。
        $sort:
            排序文档
        $geoNear:
            选择某个地理位置附近的文档。
        $out:
            把管道的结果写入某个集合
        $redact:
            控制特定数据的访问。

```

#### 聚合-实战：
```
//根据 product_id 分组输入文档，计算每个产品的评价数量
db.reviews.aggregate([
    { $group: {_id: '$product_id',count:{$sum:1}}}
])

//查询一个商品的评论总数
db.reviews.aggregate([
    { $match:{product_id:"1111"}},
    { $group: {_id: '$product_id',count:{$sum:1}}}
])

//计算平均分
db.reviews.aggregate([
    { $match:{product_id:"1111"}},
    { $group: {_id: '$product_id',count:{$sum:1},average:{$avg:'$reating'}}}
])

//查询某个商品评论：
    评论 3分的有 1
    评论 4分的有 3 
db.reviews.aggregate([
    { $match:{product_id:"1111"}},
    { $group: {_id: '$reating',count:{$sum:1}}}
])

//将管道结果保存到 mainCategotySummary ，这个操作会将原始数据更新掉，注意
db.products.aggregate([
    {$group:{_id:'$main_cat_id',
              count:{$sum:1}}},
    {$out: 'products'}
])
db.products.find({});

// 获取商品id
db.products.aggregate([
    {$project:{category_ids:23231}}
])

// $unwind 
db.products.aggregate([
    {$project:{catgory_ids:23231}},
    {$unwind:'$catgory_ids'},
    {$group:{_id:'$catgory_ids',
            count:{$sum:1}}},
    {$out: 'countsByCategoty'}
])
db.countsByCategoty.find({})


// 运算符
    $in: 频繁的使用 ids 列表
    $nin: 查询不包括在值内的数据
    $all: 如果所有的参数在引用集合中被使用，则匹配上
    $ne:  不匹配参数条件
    $not: 不匹配结果
    $or: 有一个条件匹配就成立
    $nor: 所有条件都不匹配
    $and: 所有条件都匹配
    $exists: 判断元素是否存在
    $size: 查询集合的大小
    $where:

// group 函数
$addToSet : 为组里唯一的值创建一个数组
$first: 组里的第一个值，只有前缀 $sort 才有意义。
$last: 组里最后一个值，只有前缀是 $sort 才有意义。
$max: 组里某个字段的最大值。
$min: 组里某个字段的最小值。
$avg: 某个字段的平均值。
$push: 返回组内所有值的数组，不去除重复值。
$sum: 求组内所有值的和。

// 字符串函数
$concat: 连接2个或者更多字符串为一个字符串。
$strcasecmp: 大小写敏感的比较，返回数字。
$substr: 获取字符串的子串。
$toLower: 转换为小写字符串。
$toUpper: 转换为大写字符串。

// 算术运算函数
$add : 求和
$divide : 除法
$mod: 求余数
$multiply: 乘
$subtract: 减

// 逻辑函数
$add true : 与操作，如果数组中所有值都为 true,则返回 true
$cmp : 如果两个数相等就返回 0
$cond if... then... else : 条件逻辑
$eq: 两个值是否相等
$gt: 值1是否大于值2
$gte: 值1是否大于等于值2 
$ifNull: 把null值转化成特定的值
$lt: 值1是否小于2 
$lte: 值1是否小于等于2
$ne: 值1是否不等于值2
$not: 取反操作
$or: 或
$cond 函数和三元表达式差不多

//集合操作
$setEquals: 如果两个集合的元素完全相同，则为true。
$setIntersection: 返回两个集合的公共元素。
$setDifference: 返回第一个几个中与第二个集合中不同的元素。
$setUnion: 合并集合
$setIsSubset: 如果第二个集合为第一个集合的子集，则为true
$anyElementTrue: 如果某个集合元素为 ture,则为true
$allElementsTrue true :如果所有集合元素都为 true,则为true.

//其他操作符
db.tree.distinct('sku');

// map-reduce

```