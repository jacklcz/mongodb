# **MongoDB使用- remove\(\)函数删除数据**

## **描述**

MongoDB集合的删除。

**提示**：在执行remove前先执行find\(\)命令来判断执行的条件是否正确，这是一个比较好的习惯。

## **查看集合中已经插入的数据**

```
> db.userinfo.find();
```

## **使用 remove\(\) 函数移除数据**

如果你想移除"userdetails"集合中"user\_id" 为 "testuser"的数据你可以执行以下命令：

```
> db.userinfo.remove( { "userId" : 1 } )
```

## **删除所有数据**

如果你想删除"userinfo"集合中的所有数据，可以执行以下命令：

```
> db.userinfo.remove({})
```

## **使用drop\(\)删除集合**

如果你想删除整个"userinfo"集合，包含所有文档数据，可以执行以下数据：

```
> db.userinfo.drop()
```

drop\(\)函数返回 true或者false。以上执行结果返回了true，说明操作成功。

## **使用dropDatabase\(\)函数删除数据库**

如果你想删除整个数据库的数据，你可以执行以下命令：

```
> db.dropDatabase()
```

执行命令前查看当前使用的数据库是一个良好的习惯，这样可以确保你要删除数据库是正确的，以免造成误操作而产生数据丢失的后果：

