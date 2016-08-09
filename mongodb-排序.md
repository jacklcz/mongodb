# **MongoDB 排序**

## **MongoDB sort\(\)方法**

在MongoDB中使用使用sort\(\)方法对数据进行排序，sort\(\)方法可以通过参数指定排序的字段，并使用 1 和 -1 来指定排序的方式，其中 1 为升序排序，而-1是用于降序排列。

### **语法**

sort\(\)方法基本语法如下所示：

```
>db.COLLECTION_NAME.find().sort({KEY:1})

```

### **实例**

userinfo 集合中的数据如下：

```
{ "_id" : ObjectId("57a07aace6cf836271b9b597"), "userId" : 21, "age" : 39 }
{ "_id" : ObjectId("57a07aace6cf836271b9b598"), "userId" : 22, "age" : 40 }
{ "_id" : ObjectId("57a07aace6cf836271b9b599"), "userId" : 23, "age" : 41 }
{ "_id" : ObjectId("57a07aace6cf836271b9b59a"), "userId" : 24, "age" : 42 }
{ "_id" : ObjectId("57a07aace6cf836271b9b59b"), "userId" : 25, "age" : 43 }
{ "_id" : ObjectId("57a07aace6cf836271b9b59c"), "userId" : 26, "age" : 44 }
{ "_id" : ObjectId("57a07aace6cf836271b9b59d"), "userId" : 27, "age" : 45 }
{ "_id" : ObjectId("57a07aace6cf836271b9b59e"), "userId" : 28, "age" : 46 }
```

```
>db.userinfo.find({},{"title":1,_id:0}).sort({"title":-1})
{"title":"Tutorials Point Overview"}
{"title":"NoSQL Overview"}
{"title":"MongoDB Overview"}
>

```

**注：** 如果没有指定sort\(\)方法的排序方式，默认按照文档的升序排序

