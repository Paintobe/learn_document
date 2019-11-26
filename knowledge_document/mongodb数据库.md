## mongodb数据库

## 一 安装

去到mongodb的官网  点击 for free 选择你要下载的版本

下载mongodb的版本 需要俩点注意

1. 根据业界规则 偶数为稳定版 如3.4.x  奇数为开发版 如1.7.x
2. 32bit的mongodb最大值呢个存放2G的数据   64bit就没一限制



## 二、进入mongodb数据库

windows下

#### (1) 开启服务

cd mongodb的bin目录

输入 mongod.exe --dbpath=创建mongodb数据库的位置

#### (2) 重新打开一个终端

cd mongodb的bin目录

输入 mongo.exe

此刻就进入到mongodb的数据库了

ubuntu

sudo apt-get install mongodb

也可以去mongodb官网 去下载 在解压安装



## 三、json和bson类型

#### JSON：

JSON 是一种被广泛使用的轻量级的数据交换格式 支持现今绝大多数的主流开发语言  而近几年mongodb则采用了类json的数据格式   在json上 进行了丰富和增强  使得mongodb可以处理更大的数据类型

**格式：**
{“key”:"value"}

**BSON：**

特性：轻量形  可变厉形  高效形

什么是BSON：

BSON是一个类json的一种二进制形式存储的数据格式 简称binary Json



## 四、NoSQl

NoSQL 意味着 不仅仅是SQL == Not Only SQL

mongodb将数据存储为一个文档  数据结构由 key==>value 键值对组成  字段的值 可以包含其它文档 数组 及数组文档



## 五、MongoDB概念解析

| SQL术语/概念 | MongoDB术语/概念 | 解释说明                              |
| ------------ | ---------------- | ------------------------------------- |
| database     | database         | 数据库                                |
| table        | collection       | 数据库表/集合                         |
| row          | document         | 数据记录行/文档                       |
| column       | field            | 数据字段/域                           |
| index        | index            | 索引                                  |
| table joins  |                  | 表链接/不支持                         |
| primary key  | primary key      | 主键 mongodbdb自动将_id字段设置为主键 |



## 六、数据类型

下面为mongodb中常用的几种数据类型：

1. object id  文档ID
2. string 字符串 最常用  必须是有效的UTF-8
3. Boolean 存储一个bool值  true或false
4. integer 整数可以是32位或者是64位的
5. double 存储浮点数
6. array 数组/列表  多个值存储到一个键
7. object 用于嵌入式的文档    也就是一个值为一个文档
8. null 存储null值
9. TimeStamp 时间戳

**注意事项：**

1. 文档中的键值对 是有序的
2. 文档终端额值 不仅可以是爽引号里面的字符串 还可以是其它类型   甚至可以是一个文档
3. mongodb区分类型和大小写
4. mongodb的文档的key是不可以有重复的
5. 以_开头的键 是保留的



## 七、对于库和集合的操作

(1) 查看所有的库

show dbs

(2) 选择数据库 

use 数据库名称

**注意：**

如果选择的数据库不存在 则为创建数据库  存在则为切换

使用use创建的数据库是看不到的 除非在数据库中创建集合 可以通过db/db.getName() 去进行查看当前所在的库

(3) 创建集合(也就是创建表)

db.createCollection('集合名称')

(4) 查看所有的集合

show collections

(5) 删除集合

db.集合名.drop()

(6) 删除数据库

db.dropDatabase()

**注意：**

1. 在mongodb数据库里 对于文档 集合的操作  统一使用  db（代表当前的库）
2. 严格区分大小写
3. 退出之前 最好use一下 或者db一下  查看自己当前所在的库





## 八、INSERT/SAVE文档的添加

**注意：**

如果是单纯的作为数据的添加  建议使用insert  我们的save也可以作为数据的添加  但是主要作为数据的修改

#### (1) 使用insert插入数据

**插入一条**

db.集合名.insert(文档)

**实例**

db.user.insert({'name':'lucky','age':18,'sex':'男'})

**插入多条**

db.集合名.insert([文档1,文档2...])

**实例**

db.user.insert([{'name':'王五','age':20,'sex':'男'},{name:'李四',age:30,sex:'女'}])

**注意：**

1. 如果插入多条没有给数组 则为插入第一条数据
2. key 的引号可加可不加  但是如果是python操作mongodb 则必须加引号 否则报错

#### 3.2版本以后 还有如下用于插入文档的方式（更加语义话）

+ db.collection.insertOne()  向指定集合中插入一条文档数据
+ db.collection.insertMany() 向指定集合中 插入多条文档数据



#### (2) 使用save

插入文档

db.collection.save(文档)

**实例：**

db.user.save({name:'xxx',age:40,sex:'女'})



修改文档(其实就是对你要修改的id的文档  进行值的覆盖)

db.collection.save({_id:(id值),key:v.....})

**实例 **

db.user.save({ "_id" : ObjectId("5ce7e28acfef3375fa66636c"), "name" : "ooo", "age" : 35, "sex" : "男" })

db.user.save({ "_id" : ObjectId("5ce7e28acfef3375fa66636c"), "name" : "oo", "age" : 25})

**注意：**

使用save进行文档的修改  会将原有的field 覆盖掉



## 九、FIND查询

#### (1) find查询所有 

**格式：**

db.collection.find(query,{field:1/0...})  query为查询的筛选条件 也就是mysql的where 其中后面的field1/0为 对某些field进行返回或者不返回 **其中参数可选**

**实例：**

**查询所有** 

db.collection.find()  === db.collection.find({})

**对某些field进行显示**

返回name域的值 

db.user.find({},{name:1/true})

**对某些field进行不显示**

除了name的field全部返回

db.user.find({},{name:0/false})

**指定_id不返回**

db.user.find({},{_id:false})

**错误的写法**

db.user.find({},{name:true,sex:false})

**注意：**

1. 我们的_id默认返回的 需要单独给\_id设置 false
2. inclusion和exclusion 俩种模式不可混用  因为这样的话 无法推断其它key是否应该返回
3. 如果不需要查询条件 则也需要使用{}进行占位
4. 1/0 也可以使用true/false 一样

#### (2) findOne 查询一条

db.collections.findOne(query,,{field:1/0...})

**实例：**

查询一条文档 返回name域的值 其余都不返回包括_id

db.user.find({},{\_id:false,name:true})

#### (3) count()  统计数据条数

**格式**

db.collections.find([query]).count()

**实例：**

db.user.find().count()

#### (4) pretty() 展开来查看

**格式：**

db.collection.find([query]).pretty()

#### (5) 查询条件操作符

| 符号               | 符号说明            | 实例                                                         | 说明                            |
| ------------------ | ------------------- | ------------------------------------------------------------ | ------------------------------- |
| $gt                | 大于                | db.collection.find({age:{$gt:18}})                           | 年龄大于18                      |
| $gte               | 大于等于            | db.collection.find({age:{$gte:18}})                          | 年龄大于等于18                  |
| $lt                | 小于                | db.collection.find({age:{$lt:18}})                           | 年龄小于18                      |
| $lte               | 小于等于            | db.collection.find({age:{$lte:18}})                          | 年龄小于等于18                  |
| key:value          | 等于                | db.collection.find({age:18})                                 | 年龄等于18                      |
| _id:ObjectId(id值) | 使用id进行查询      | db.collection.find({"_id" : ObjectId("5ce7e0e6cfef3375fa66636b")}) | 查询id为...的文档               |
| /值/               | 模糊查询            | db.collection.find({name:/lucky/})                           | 查询name中包含lucky的值的文档   |
| /^值/              | 以...某个值作为开头 | db.collection.find({name:/^lucky/})                          | 查询name中以lucky作为开头的文档 |
| /值$/              | 以...某个值作为结尾 | db.collection.find({name:/lucky$/})                          | 查询name中以lucky作为结尾的文档 |
| $in                | 在...内             | db.collection.find({age:{$in:[18,28]}})                      | 查询年龄为18 或者28的文档       |
| $nin               | 不再...内           | db.collection.find({age:{$nin:[18,28]}})                     | 查询年龄不为18 或者28的文档     |
| $ne                | 不等于              | db.collection.find({age:{$ne:18}})                           | 查询年龄不为18的文档            |

#### (6) AND 查询

**格式：**

db.collection.find({key1:v1,key2:v2....})

**实例：**

查询年龄为30的 并且name以四作为结尾的文档

db.user.find({name:/四$/,age:30})

查询age大于等于20 并且小于25

db.user.find({age:{$gte:20,$lte:25}})

查询age大于等于20 并且小于25 name为张三

db.user.find({age:{$gte:20,$lte:25},name:'张三'})

#### (7) OR 查询

**格式：**

db.collection.find({$or:[{条件1},{条件2}...]})

**实例：**

查询name为张三或者李四的文档

db.user.find({$or:[{name:'张三'},{name:'李四'}]})

查询年龄为18或者20的文档

db.user.find({$or:[{age:18},{age:20}]})

#### (8) AND和OR的组合使用

**格式：**

db.collection.find({query1,...,$or:[{query1},{query2}...]})

**实例：**

查询性别为男 年龄为18或者20的文档

db.user.find({sex:'男',$or:[{age:18},{age:20}]})

#### (9) LIMIT取值

**格式：**

从第0个开始取几条文档

db.collection.find().limit(num)

**实例：**

db.user.find().limit(2)

db.user.find().limit(2).pretty()

#### (10) skip 跳过几条文档

**格式：**

db.collecion.find().skip(num)

**实例：**

db.user.find().skip(2) 跳过俩条文档

#### (11) limit和skip的组合使用

**格式：**

db.collection.find().skip(num).limit(num)

**实例：**

跳过2条取出俩条文档

db.user.find().skip(2).limit(2)

#### (12) SORT排序

**格式：**

db.collection. find().sort({key:1/-1})    1代表升序  -1代表降序

**实例：**

按照年龄进行升序和降序

db.user.find().sort({age:1/-1})



## 十、UPDATE修改

**结构：**

```python
db.collection.update(
	<query>,
    <update>,
    {
        upsert:<boolean>,
        multi:<boolean>
    }
)
```

+ query: update的查询条件 类似sql语句中的where条件
+ update: update对象和一些更新的操作符 如：$inc $set
+ upsert: 可选  如果不存在update的记录时是否新插入 默认是false 不插入
+ multi: 可选 默认值false 只更改找到的第一条记录   如果为true 则更新全部

#### update更新操作符  $set  $inc

**$set** 直接修改

**实例：**

将name为lucky的文档 key为age的值改为5

db.user.update({name:'lucky'},{$set:{age:5}})

**$inc** 累加修改

将name为lucky的文档 key为age的值累加5

db.user.update({name:'lucky'},{$inc:{age:5}})

**multi参数的使用**

将所有的文档中age的值累加5

db.user.update({},{$inc:{age:5}},{multi:true})

**upsert参数的使用**

修改name为苍苍的文档中age的值改为20  如果该条记录不存在  则作为新文档插入

db.user.update({name:'苍苍'},{$set:{age:20}},{upsert:true})

**multi和upsert组合使用**

将所有的文档中age的值累加5

db.user.update({},{$inc:{age:5}},false,true)

#### 3.2版本以后

db.collection.updateOne()   更新一条

db.collection.updateMany(query,update,true/false) 第三个参数为upsert



## 十一、REMOVE文档的删除

**主体结构：**

```python
db.collection.remove(
	<query>,
    {
        justOne:<boolean>
    }
)
```

**参数说明：**

+ query :可选  删除文档的条件
+ justOne 可选 如果设为true 或者1  则只删除一个文档  默认false

**实例：**

db.collection.remove({条件})  默认将所有匹配到的文档进行删除

db.collection.remove({条件},true/1) 只删除第一个匹配到的文档

db.collection.remove({条件},{justOne:true})  只删除第一个匹配到的文档

删除年龄在30到40之间的文档

db.user.remove({age:{$gte:30,$lte:40}})

删除所有文档

db.collection.remove({})

#### 3.2版本以后

remove() 方法现在已经过时 推荐使用以下方法

+ deleteOne() 删除一条
+ deleteMany() 删除多条



