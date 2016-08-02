# **MongoDB 数据插入**

## **描述**

本章节中我们将向大家介绍如何将数据插入到MongoDB的集合中。

文档的数据结构和JSON基本一样。

所有存储在集合中的数据都是BSON格式。

BSON是一种类json的一种二进制形式的存储格式,简称Binary JSON。

## **MongoDB数据库切换**

以下命令可以使用"mytest"数据库：

```
use mytest; 
>switch to db mytest;
```

## **为MongoDB数据库定义一个文档**

```
>document=({"userId":"1","name":"LiangChengZhu","age":18})
```

**在集合中插入文档**

将以上的文档数据存储到"mytest" 数据库中的 "userinfo" 集合，执行如下命令

```
>db.userinfo.insert(document);

>show collections; //查看当前db所有集合
```





## **使用javaScript 批量插入文档**



![](/assets/A80F8C17-9497-47FC-A5E1-8760CFEEFDA9.png)

