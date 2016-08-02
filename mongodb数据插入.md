# **MongoDB 数据插入**

## **描述**

本章节中我们将向大家介绍如何将数据插入到MongoDB的集合中。

文档的数据结构和JSON基本一样。

所有存储在集合中的数据都是BSON格式。

BSON是一种类json的一种二进制形式的存储格式,简称Binary JSON。

## **MongoDB数据库切换**

以下命令可以使用"mytest"数据库：

```
use mytest; switch to db mytest;
```

## **为MongoDB数据库定义一个文档**

以下文档可以存储在MongoDB中：

```
document=({"userId":"1","name":"LiangChengZhu","age":18})
```

命令执行如下图所示：

## **显示已定义的文档**

已定义的文档显示格式如下所示：

## **在集合中插入文档**

将以上的文档数据存储到"myinfo" 数据库中的 "userdetails" 集合，执行如下命令：

```
db.userdetails.insert(document)

```

## **使用换行符插入数据**

当文档的数据较多的时候，我们可以使用换行符来分割文档数据，如下所示：

```
document=({"user_id" : "ABCDBWN","password" :"ABCDBWN" ,"date_of_join" : "15/10/2010" ,  
"education" :"B.C.A." , "profession" : "DEVELOPER","interest" : "MUSIC",  
"community_name" :["MODERN MUSIC", "CLASSICAL MUSIC","WESTERN MUSIC"],  
"community_moder_id" : ["MR. BBB","MR. JJJ","MR MMM"],  
"community_members" : [500,200,1500],"friends_id" : ["MMM123","NNN123","OOO123"],  
"ban_friends_id" :["BAN123","BAN456","BAN789"]});

```

命令执行如下图所示：

## **集合中直接插入数据（无定义文档）**

数据可以不用定义文档通过shell直接插入：

```
db.userdetails.insert({"user_id" : "xyz123","password" :"xyz123" ,"date_of_join" : "15/08/2010" ,  
"education" :"M.C.A." , "profession" : "Software consultant","interest" : "Film",  
"community" : [  
{  
"name" : "DDD FILM CLUB",  
"moder_id" : "MR. DBNA",  
"members" : "25000",  
},  
{  
"name" : "AXN MOVIES",  
"moder_id" : "DOGLUS HUNT",  
"members" : "15000",  
},  
{  
"name" : "UROPEAN FILM LOVERS",  
"moder_id" : "AMANT LUIS",  
"members" : "20000",  
}  
],  
"friends" :[  
{  
"user_id" : "KKK258",  
},  
{  
"user_id" : "LLL147",  
},  
{  
"user_id" : "MMM369",  
}  
],  
"ban_friends" :[  
{  
"user_id" : "BAN147"  
},  
{  
"user_id" : "BAN258"  
},  
{  
"user_id" : "BAN369"  
}  
]  
});

```

命令执行如下图所示：

## **查看集合中的数据**

使用以下命令查看集合中的数据：

```
db.userdetails.find();

```

