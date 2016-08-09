# **MongoDB 聚合**

MongoDB中聚合\(aggregate\)主要用于处理数据\(诸如统计平均值,求和等\)，并返回计算后的数据结果。有点类似sql语句中的 count\(\*\)。

## **aggregate\(\) 方法**

MongoDB中聚合的方法使用aggregate\(\)。

### **语法**

aggregate\(\) 方法的基本语法格式如下所示：

```
>db.COLLECTION_NAME.aggregate(AGGREGATE_OPERATION)

```

### **实例**

userinfo集合中的数据如下：

```
{
{ "_id" : ObjectId("57a07aace6cf836271b9b597"), "userId" : 21, "age" : 39 }
{ "_id" : ObjectId("57a07aace6cf836271b9b598"), "userId" : 22, "age" : 40 }
{ "_id" : ObjectId("57a07aace6cf836271b9b599"), "userId" : 23, "age" : 41 }
{ "_id" : ObjectId("57a07aace6cf836271b9b59a"), "userId" : 24, "age" : 42 }
{ "_id" : ObjectId("57a07aace6cf836271b9b59b"), "userId" : 25, "age" : 43 }
{ "_id" : ObjectId("57a07aace6cf836271b9b59c"), "userId" : 26, "age" : 44 }
{ "_id" : ObjectId("57a07aace6cf836271b9b59d"), "userId" : 27, "age" : 45 }
{ "_id" : ObjectId("57a07aace6cf836271b9b59e"), "userId" : 28, "age" : 46 }
{ "_id" : ObjectId("57a07aace6cf836271b9b59f"), "userId" : 29, "age" : 47 }
{ "_id" : ObjectId("57a07aace6cf836271b9b5a0"), "userId" : 30, "age" : 48 }
{ "_id" : ObjectId("57a07aace6cf836271b9b5a1"), "userId" : 31, "age" : 49 }
{ "_id" : ObjectId("57a07aace6cf836271b9b5a2"), "userId" : 32, "age" : 50 }
{ "_id" : ObjectId("57a07aace6cf836271b9b5a3"), "userId" : 33, "age" : 51 }
{ "_id" : ObjectId("57a07aace6cf836271b9b5a4"), "userId" : 34, "age" : 52 }
{ "_id" : ObjectId("57a07aace6cf836271b9b5a5"), "userId" : 35, "age" : 53 }
{ "_id" : ObjectId("57a07aace6cf836271b9b5a6"), "userId" : 36, "age" : 54 }

```

我们先来新增方便group\(分组\)的一个 school 学校字段。

```
db.userinfo.update({"userId":{$gt:50}}, {$set: {"school": 'Tsinghua'}}, {multi: 1});
db.userinfo.update({"userId":{$lt:50}}, {$set: {"school": 'PKU'}}, {multi: 1});
```

现在我们通过以上集合计算按照学校分组的总人数，使用aggregate\(\)计算结果如下：

```
> db.userinfo.aggregate([{$group : {_id : "$school", count_user : {$sum : 1}}}]);
{ "_id" : "Tsinghua", "count_user" : 49 }
{ "_id" : "PKU", "count_user" : 49 }

```

在上面的例子中，我们通过字段school字段对数据进行分组。

下表展示了一些聚合的表达式:

| **表达式描述实例** |  |  |
| :--- | :--- | :--- |
| $sum | 计算总和。 | db.mycol.aggregate\(\[{$group : {\_id : "$by\_user", num\_tutorial : {$sum : "$likes"}}}\]\) |
| $avg | 计算平均值 | db.mycol.aggregate\(\[{$group : {\_id : "$by\_user", num\_tutorial : {$avg : "$likes"}}}\]\) |
| $min | 获取集合中所有文档对应值得最小值。 | db.mycol.aggregate\(\[{$group : {\_id : "$by\_user", num\_tutorial : {$min : "$likes"}}}\]\) |
| $max | 获取集合中所有文档对应值得最大值。 | db.mycol.aggregate\(\[{$group : {\_id : "$by\_user", num\_tutorial : {$max : "$likes"}}}\]\) |
| $push | 在结果文档中插入值到一个数组中。 | db.mycol.aggregate\(\[{$group : {\_id : "$by\_user", url : {$push: "$url"}}}\]\) |
| $addToSet | 在结果文档中插入值到一个数组中，但不创建副本。 | db.mycol.aggregate\(\[{$group : {\_id : "$by\_user", url : {$addToSet : "$url"}}}\]\) |
| $first | 根据资源文档的排序获取第一个文档数据。 | db.mycol.aggregate\(\[{$group : {\_id : "$by\_user", first\_url : {$first : "$url"}}}\]\) |
| $last | 根据资源文档的排序获取最后一个文档数据 | db.mycol.aggregate\(\[{$group : {\_id : "$by\_user", last\_url : {$last : "$url"}}}\]\) |

## 

