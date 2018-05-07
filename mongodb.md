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



