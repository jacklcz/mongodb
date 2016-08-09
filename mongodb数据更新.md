# **MongoDB使用update\(\)函数更新数据**

## **描述**

MongoDB数据更新可以使用update\(\)函数。

```
db.collection.update( criteria, objNew, upsert, multi )

```

update\(\)函数接受以下四个参数：

* **criteria** : update的查询条件，类似sql update查询内where后面的。
* **objNew** : update的对象和一些更新的操作符（如$,$inc...）等，也可以理解为sql update查询内set后面的
* **upsert** : 这个参数的意思是，如果不存在update的记录，是否插入objNew,true为插入，默认是false，不插入。
* **multi** : mongodb默认是false,只更新找到的第一条记录，如果这个参数为true,就把按条件查出来多条记录全部更新。

**update\(\) 命令**

如果我们想将"userinfo"集合中"userId"为"1"的"name"字段修改为"91JINRONG"，那么我们可以使用update\(\)命令来实现（如下实例所示）。 db.idStock.update\({'\_id’:'Asking'},{$set:{'value':NumberLong\(100003\)}}\)

```
> db.userinfo.update({'userId':"1"},{$set:{"name":"91jinrong"}})
```

如果upsert设置为true , 并且没有找到更新条件的数据，mongodb会插入新的纪录:

```
> db.userinfo.update({'userId':101},{$set:{"name":"SUNLONGLONG"}},true,false)
```

以下实例将更新第一条匹配条件的数据：

```
> db.userinfo.update({'userId':{$gt:95}},{$set:{"name":"SUNLONGLONG123"}},true,false)
```

以下实例将更新全部匹配条件的数据：

```
> db.userinfo.update({'userId':{$gt:95}},{$set:{"name":"SUNLONGLONG123"}},true,true)
```

## **查看集合中更新后的数据**

我们可以使用以下命令查看数据是否更新：

```
> db.userinfo.find();

```

## 

