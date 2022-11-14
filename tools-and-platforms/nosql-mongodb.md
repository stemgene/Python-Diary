# NoSQL-MongoDB

## 一、基本操作

### 1. 1 创建collection

```
db.createCollection(name, options)
> db.createCollection("runoob")
{ "ok" : 1 }
```

或使用Mongoose

```javascript
const TodoSchema = new Schema({
    text: {
        type: String,
        required: true,
    },
    complete: {
        type: Boolean,
        default: false,
    },
    timestamp: {
        type: String,
        default: Date.now()
    }
})

const Todo = mongoose.model("Todo", TodoSchema);
```

### 1.2 插入document

MongoDB 使用 insert() 或 save() 方法向集合中插入文档，

```
db.COLLECTION_NAME.insert(document)
db.COLLECTION_NAME.insertOne(document)
db.collection.insertMany(
   [ <document 1> , <document 2>, ... ],
   {
      writeConcern: <document>,
      ordered: <boolean>
   }
)
```

### 1.3 查询find

```
db.collection.find(query, projection)
查询 name 中包含 mongo 的数据 模糊查询用于搜索
db.user.find({"name": /mongo/});
查询 name 中以 mongo 开头的
db.user.find({"name": /^mongo/});
查询 name 中以 mongo 结尾的
db.user.find({"name": /mongo$/});
```

| 操作    | 格式                       | 范例                          | RDBMS中的类似语句         |
| ----- | ------------------------ | --------------------------- | ------------------- |
| 等于    | `{<key>:<value>`}        | `find({"by":"菜鸟教程"})`       | `where by = '菜鸟教程'` |
| 小于    | `{<key>:{$lt:<value>}}`  | `find({"likes":{$lt:50}})`  | `where likes < 50`  |
| 小于或等于 | `{<key>:{$lte:<value>}}` | `find({"likes":{$lte:50}})` | `where likes <= 50` |
| 大于    | `{<key>:{$gt:<value>}}`  | `find({"likes":{$gt:50}})`  | `where likes > 50`  |
| 大于或等于 | `{<key>:{$gte:<value>}}` | `find({"likes":{$gte:50}})` | `where likes >= 50` |
| 不等于   | `{<key>:{$ne:<value>}}`  | `find({"likes":{$ne:50}})`  | `where likes != 50` |

MongoDB 的 find() 方法可以传入多个键(key)，每个键(key)以逗号隔开，即常规 SQL 的 AND 条件。

```
db.col.find({"by":"菜鸟教程", "title":"MongoDB 教程"})
```

MongoDB OR 条件语句使用了关键字 **$or**,语法格式如下：

```
>db.col.find(
   {
      $or: [
         {key1: value1}, {key2:value2}
      ]
   }
)
```

### 1.3 更新

MongoDB 使用 **update()** 和 **save()** 方法来更新集合中的文档。

```
db.col.update({'title':'MongoDB 教程'},{$set:{'title':'MongoDB'}})
```

save() 方法通过传入的文档来替换已有文档，\_id 主键存在就更新，不存在就插入。

## 二、聚合

MongoDB 中聚合(aggregate)主要用于处理数据(诸如统计平均值，求和等)，并返回计算后的数据结果。有点类似 **SQL** 语句中的 count(\*)。

### 2.1 aggregate

```
>db.COLLECTION_NAME.aggregate(AGGREGATE_OPERATION)
>db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$sum : 1}}}])
以上类似MySQL中的：
 select by_user, count(*) from mycol group by by_user
```



| 表达式       | 描述                                        | 实例                                                                                         |
| --------- | ----------------------------------------- | ------------------------------------------------------------------------------------------ |
| $sum      | 计算总和。                                     | db.mycol.aggregate(\[{$group : {\_id : "$by\_user", num\_tutorial : {$sum : "$likes"\}}}]) |
| $avg      | 计算平均值                                     | db.mycol.aggregate(\[{$group : {\_id : "$by\_user", num\_tutorial : {$avg : "$likes"\}}}]) |
| $min      | 获取集合中所有文档对应值得最小值。                         | db.mycol.aggregate(\[{$group : {\_id : "$by\_user", num\_tutorial : {$min : "$likes"\}}}]) |
| $max      | 获取集合中所有文档对应值得最大值。                         | db.mycol.aggregate(\[{$group : {\_id : "$by\_user", num\_tutorial : {$max : "$likes"\}}}]) |
| $push     | 将值加入一个数组中，不会判断是否有重复的值。                    | db.mycol.aggregate(\[{$group : {\_id : "$by\_user", url : {$push: "$url"\}}}])             |
| $addToSet | 将值加入一个数组中，会判断是否有重复的值，若相同的值在数组中已经存在了，则不加入。 | db.mycol.aggregate(\[{$group : {\_id : "$by\_user", url : {$addToSet : "$url"\}}}])        |
| $first    | 根据资源文档的排序获取第一个文档数据。                       | db.mycol.aggregate(\[{$group : {\_id : "$by\_user", first\_url : {$first : "$url"\}}}])    |
| $last     | 根据资源文档的排序获取最后一个文档数据                       | db.mycol.aggregate(\[{$group : {\_id : "$by\_user", last\_url : {$last : "$url"\}}}])      |

## Join操作

```javascript
{
   $lookup:
     {
       from: <collection to join>,
       localField: <field from the input documents>,
       foreignField: <field from the documents of the "from" collection>,
       as: <output array field>
     }
}
```

