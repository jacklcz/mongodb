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



现在我们通过以上集合计算平均age，使用aggregate\(\)计算结果如下：

```
> db.userinfo.aggregate([{$group : {_id : "$by_user", count_age : {$sum : 1}}}])
{
   "result" : [
      {
         "_id" : "w3cschool.cc",
         "num_tutorial" : 2
      },
      {
         "_id" : "Neo4j",
         "num_tutorial" : 1
      }
   ],
   "ok" : 1
}
>

```

以上实例类似sql语句： _select by\_user, count\(\*\) from mycol group by by\_user_

在上面的例子中，我们通过字段by\_user字段对数据进行分组，并计算by\_user字段相同值的总和。

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

## **管道的概念**

管道在Unix和Linux中一般用于将当前命令的输出结果作为下一个命令的参数。

MongoDB的聚合管道将MongoDB文档在一个管道处理完毕后将结果传递给下一个管道处理。管道操作是可以重复的。

表达式：处理输入文档并输出。表达式是无状态的，只能用于计算当前聚合管道的文档，不能处理其它的文档。

这里我们介绍一下聚合框架中常用的几个操作：

* $project：修改输入文档的结构。可以用来重命名、增加或删除域，也可以用于创建计算结果以及嵌套文档。
* $match：用于过滤数据，只输出符合条件的文档。$match使用MongoDB的标准查询操作。
* $limit：用来限制MongoDB聚合管道返回的文档数。
* $skip：在聚合管道中跳过指定数量的文档，并返回余下的文档。
* $unwind：将文档中的某一个数组类型字段拆分成多条，每条包含数组中的一个值。
* $group：将集合中的文档分组，可用于统计结果。
* $sort：将输入文档排序后输出。
* $geoNear：输出接近某一地理位置的有序文档。

### **管道操作符实例**

1、$project实例

```
db.article.aggregate(
    { $project : {
        title : 1 ,
        author : 1 ,
    }}
 );

```

这样的话结果中就只还有\_id,tilte和author三个字段了，默认情况下\_id字段是被包含的，如果要想不包含\_id话可以这样:

```
db.article.aggregate(
    { $project : {
        _id : 0 ,
        title : 1 ,
        author : 1
    }});

```

2.$match实例

```
db.articles.aggregate( [
                        { $match : { score : { $gt : 70, $lte : 90 } } },
                        { $group: { _id: null, count: { $sum: 1 } } }
                       ] );

```

$match用于获取分数大于70小于或等于90记录，然后将符合条件的记录送到下一阶段$group管道操作符进行处理。

3.$skip实例

```
db.article.aggregate(
    { $skip : 5 });

```

经过$skip管道操作符处理后，前五个文档被"过滤"掉。

