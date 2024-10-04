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

<table><thead><tr><th width="106">操作</th><th width="257">格式</th><th width="289">范例</th><th>RDBMS中的类似语句</th></tr></thead><tbody><tr><td>等于</td><td><code>{&#x3C;key>:&#x3C;value></code>}</td><td><code>find({"by":"菜鸟教程"})</code></td><td><code>where by = '菜鸟教程'</code></td></tr><tr><td>小于</td><td><code>{&#x3C;key>:{$lt:&#x3C;value>}}</code></td><td><code>find({"likes":{$lt:50}})</code></td><td><code>where likes &#x3C; 50</code></td></tr><tr><td>小于或等于</td><td><code>{&#x3C;key>:{$lte:&#x3C;value>}}</code></td><td><code>find({"likes":{$lte:50}})</code></td><td><code>where likes &#x3C;= 50</code></td></tr><tr><td>大于</td><td><code>{&#x3C;key>:{$gt:&#x3C;value>}}</code></td><td><code>find({"likes":{$gt:50}})</code></td><td><code>where likes > 50</code></td></tr><tr><td>大于或等于</td><td><code>{&#x3C;key>:{$gte:&#x3C;value>}}</code></td><td><code>find({"likes":{$gte:50}})</code></td><td><code>where likes >= 50</code></td></tr><tr><td>不等于</td><td><code>{&#x3C;key>:{$ne:&#x3C;value>}}</code></td><td><code>find({"likes":{$ne:50}})</code></td><td><code>where likes != 50</code></td></tr></tbody></table>

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



<table><thead><tr><th width="99.33333333333331">表达式</th><th>描述</th><th>实例</th></tr></thead><tbody><tr><td>$sum</td><td>计算总和。</td><td>db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$sum : "$likes"}}}])</td></tr><tr><td>$avg</td><td>计算平均值</td><td>db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$avg : "$likes"}}}])</td></tr><tr><td>$min</td><td>获取集合中所有文档对应值得最小值。</td><td>db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$min : "$likes"}}}])</td></tr><tr><td>$max</td><td>获取集合中所有文档对应值得最大值。</td><td>db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$max : "$likes"}}}])</td></tr><tr><td>$push</td><td>将值加入一个数组中，不会判断是否有重复的值。</td><td>db.mycol.aggregate([{$group : {_id : "$by_user", url : {$push: "$url"}}}])</td></tr><tr><td>$addToSet</td><td>将值加入一个数组中，会判断是否有重复的值，若相同的值在数组中已经存在了，则不加入。</td><td>db.mycol.aggregate([{$group : {_id : "$by_user", url : {$addToSet : "$url"}}}])</td></tr><tr><td>$first</td><td>根据资源文档的排序获取第一个文档数据。</td><td>db.mycol.aggregate([{$group : {_id : "$by_user", first_url : {$first : "$url"}}}])</td></tr><tr><td>$last</td><td>根据资源文档的排序获取最后一个文档数据</td><td>db.mycol.aggregate([{$group : {_id : "$by_user", last_url : {$last : "$url"}}}])</td></tr></tbody></table>

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

