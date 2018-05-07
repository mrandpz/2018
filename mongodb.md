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

9. 在 MongoDB 中，你不需要创建集合。当你插入一些文档时，MongoDB 会自动创建集合。

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

update\(\) 方法用于更新已存在的文档

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



























