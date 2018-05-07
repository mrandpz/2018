1.安装好mongoDB后，需要在mongoDB的文件目录bin下

```
mongod --dbpath d:\data\db
```

2.bin目录下执行

```
mongo.exe
```

3.显示所有数据列表

```
show dbs
```

4.连接到指定的数据库，如果没有，则是创建数据库

```
use xxx
```

* 不得含有' '（空格\)、.、$、/、\和\0 \(空字符\)。
* 应全部小写。
* 最多64字节
* 不能是空字符串（""\)。

5.对应关系

| 数据库 | 数据库 |
| :--- | :--- |
| 表格table | 集合collection |
| 行 | 文档 |
| 列 | 字段 |
| 表联合 | 嵌入文档 |

6.删除当前数据库

```
db.dropDatabase()
```

7.删除集合

```
show tables 显示当前数据库的表
db.site.drop() 删除集合site
```

8 创建集合

```
db.createCollection(name, options)
```

* options: 可选参数, 指定有关内存大小及索引的选项
* name: 要创建的集合名称

创建固定集合 mycol，整个集合空间大小 6142800 KB, 文档最大个数为 10000 个。

```
db.createCollection("mycol", { capped : true, autoIndexId : true, size :6142800, max : 10000 } )
```

**当**capped**为 true 时，必须指定 size 参数。**

1. 在 MongoDB 中，你不需要创建集合。当你插入一些文档时，MongoDB 会自动创建集合。

```
db.mycol2.insert({"name" : "菜鸟教程"})
show collections
```

10.查看集合

```
show collections
```

11.插入文档:MongoDB 使用 insert\(\) 或 save\(\) 方法向集合中插入文档，语法如下：

```
db.col.insert({title:'mongoDB',by:'your dad',url:'hah'})
```

查询已插入文档

```
db.col.find()
db.col.find().pretty()  美化显示
```

我们也可以将数据定义为一个变量，如下所示：

```
document=({title: 'MongoDB 教程', 
    description: 'mongoDB',
    likes: 'i like'
});
db.col.insert(document)
```

再次查询得

```
{ "_id" : ObjectId("5af05b0aee57d354086f5667"), "title" : "mongoDB", "by" : "you
r dad", "url" : "hah" }
{ "_id" : ObjectId("5af05b9cee57d354086f5668"), "title" : "11", "like" : "22" }
>
```

12.MongoDB 使用 update\(\) 和 save\(\) 方法来更新集合中的文档

* update\(\) 方法用于更新已存在的文档

```
db.collection.update(
   <query>,
   <update>,
   {
     upsert: <boolean>,
     multi: <boolean>,
     writeConcern: <document>
   }
)
```

**query**: update的查询条件，类似sql update查询内where后面的。

**update**: update的对象和一些更新的操作符（如$,$inc...）等，也可以理解为sql update查询内set后面的

**upsert**: 可选，这个参数的意思是，如果不存在update的记录，是否插入objNew,true为插入，默认是false，不插入。

**multi**: 可选，mongodb 默认是false,只更新找到的第一条记录，如果这个参数为true,就把按条件查出来多条记录全部更新。

**writeConcern**:可选，抛出异常的级别。

```
db.col.update({'title':'MongoDB 教程'},{$set:{'title':'MongoDB'}})
```

以上语句只会修改第一条发现的文档，如果你要修改多条相同的文档，则需要设置 multi 参数为 true。

```
db.col.update({'title':'MongoDB 教程'},{$set:{'title':'MongoDB'}},{multi:true})
```

* save方法

```
db.collection.save(
   <document>,
   {
     writeConcern: <document>
   }
)
```

```
db.col.save({
    "_id" : ObjectId("56064f89ade2f21f36b03136"),
    "title" : "MongoDB",
    "description" : "MongoDB 是一个 Nosql 数据库",
    "by" : "Runoob",
    "url" : "http://www.runoob.com",
    "tags" : [
            "mongodb",
            "NoSQL"
    ],
    "likes" : 110
})
```

## 更多实例，可查看下面后再回来看

只更新第一条记录：

db.col.update\( { "count" : { $gt : 1 } } , { $set : { "test2" : "OK"} } \);

全部更新：

db.col.update\( { "count" : { $gt : 3 } } , { $set : { "test2" : "OK"} },false,true \);

只添加第一条：

db.col.update\( { "count" : { $gt : 4 } } , { $set : { "test5" : "OK"} },true,false \);

全部添加加进去:

db.col.update\( { "count" : { $gt : 5 } } , { $set : { "test5" : "OK"} },true,true \);

全部更新：

db.col.update\( { "count" : { $gt : 15 } } , { $inc : { "count" : 1} },false,true \);

只更新第一条记录：

db.col.update\( { "count" : { $gt : 10 } } , { $inc : { "count" : 1} },false,false \);

13.MongoDB remove\(\)函数是用来移除集合中的数据。

```
db.collection.remove(
   <query>,
   {
     justOne: <boolean>,
     writeConcern: <document>
   }
)

query :（可选）删除的文档的条件。
justOne : （可选）如果设为 true 或 1，则只删除一个文档。
writeConcern :（可选）抛出异常的级别。
```

```
db.col.remove({'title':'11'})
```

删除所有

```
db.col.remove({})
```

14.MongoDB 查询数据的语法格式

| 操作 |
| :--- |


|  | 格式 | 范例 | RDBMS中的类似语句 |
| :--- | :--- | :--- | :--- |
| 等于 | `{<key>:<value>`} | `db.col.find({"by":"菜鸟教程"}).pretty()` | `where by = '菜鸟教程'` |
| 小于 | `{<key>:{$lt:<value>}}` | `db.col.find({"likes":{$lt:50}}).pretty()` | `where likes < 50` |
| 小于或等于 | `{<key>:{$lte:<value>}}` | `db.col.find({"likes":{$lte:50}}).pretty()` | `where likes <= 50` |
| 大于 | `{<key>:{$gt:<value>}}` | `db.col.find({"likes":{$gt:50}}).pretty()` | `where likes > 50` |
| 大于或等于 | `{<key>:{$gte:<value>}}` | `db.col.find({"likes":{$gte:50}}).pretty()` | `where likes >= 50` |
| 不等于 | `{<key>:{$ne:<value>}}` | `db.col.find({"likes":{$ne:50}}).pretty()` | `where likes != 50` |

MongoDB 的 find\(\) 方法可以传入多个键\(key\)，每个键\(key\)以逗号隔开，即常规 SQL 的 AND 条件。

语法格式如下：

```
db.col.find({key1:value1, key2:value2}).pretty()
```

MongoDB OR 条件语句使用了关键字**$or**,语法格式如下：

```
db.col.find(
   {
      $or: [
         {key1: value1}, {key2:value2}
      ]
   }
).pretty()
```

15.

```
MongoDB中条件操作符有：

(>) 大于 - $gt
(<) 小于 - $lt
(>=) 大于等于 - $gte
(<= ) 小于等于 - $lte
```

```
db.col.find({"likes" : {$gt : 100}})
```

```
Select * from col where likes > 100;
```

16. $type 操作符

$type操作符是基于BSON类型来检索集合中匹配的数据类型，并返回结果。

具体[查询值](http://www.runoob.com/mongodb/mongodb-operators-type.html)，

```
db.col.find({"title" : {$type : 2}})
```

17. limit 接收一个数字参数

```
db.COLLECTION_NAME.find().limit(NUMBER)
```

```
db.col.find({},{"title":1,_id:0}).limit(2)
```

18. sort基本语法 

```
db.COLLECTION_NAME.find().sort({KEY:1})
```

```
db.col.find({},{"title":1,_id:0}).sort({"likes":-1})
```

19. 索引  

```
db.COLLECTION_NAME.ensureIndex({KEY:1})
```

```
db.col.ensureIndex({"title":1})
```

ensureIndex\(\) 方法中你也可以设置使用多个字段创建索引（关系型数据库中称作复合索引）。

```
db.col.ensureIndex({"title":1,"description":-1})
```

20.聚合

```
MongoDB中聚合(aggregate)主要用于处理数据(诸如统计平均值,求和等)，并返回计算后的数据结果。有点类似sql语句中的 count(*)。
```

```
db.COLLECTION_NAME.aggregate(AGGREGATE_OPERATION)
```

示例

```
db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$sum : 1}}}])
```

管道

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

mongoDB 分片 不懂

备份与恢复

```
mongodump -h dbhost -d dbname -o dbdirectory
```

```
-h：
MongDB所在服务器地址，例如：127.0.0.1，当然也可以指定端口号：127.0.0.1:27017

-d：
需要备份的数据库实例，例如：test

-o：
备份的数据存放位置，例如：c:\data\dump，当然该目录需要提前建立，在备份完成后，系统自动在dump目录下建立一个test目录，这个目录里面存放该数据库实例的备份数据。
```

执行命令

```
mongodump
```

数据恢复 mongorestore

```
mongorestore -h <hostname><:port> -d dbname <path>
```















