## Python操作Mongodb数据库

**安装扩展库**

pip install pymongo

## 一、导入pymongo

from pymongo import MongoClient

## 二、连接服务器

mongodb端口 27017

**实例：**

```python
from pymongo import MongoClient

# 只传入主机
conn = MongoClient('127.0.0.1')

# 给主机和端口
conn = MongoClient(host='127.0.0.1',port=27017)
```

## 三、连接数据库

**实例：**

```python
# 选择数据库  conn+数据库名称
db = conn.test
```

连接集合：

collection = db[collection_name]

或者

collection = db.collection_name



## 四、插入数据

#### (1) 插入一条数据

###### db.collection.insert({文档})

**实例**

```python
# 插入一条文档
db.user.insert({"name":"lucky","age":18,"hobby":"写代码"})
```

#### (2) 插入多条文档

db.collection.insert([文档1,文档2...])

**实例**

```python
# 插入多条文档
db.user.insert([{"name":"古力娜扎","age":28,"hobby":"演戏"},{"name":"欧阳娜娜","age":20,"hobby":"拉大提琴"}])
```

#### (3) 在3.x以上建议使用

insert_one() 插入一条文档

insert_many() 插入多条文档

**获取3.x版本以上插入的Id**

res.inserted_id

res.inserted_ids

**注意：**

insert方法在插入一条和多条文档的时候 返回值为ObjectId  5cebdaa11a8f4a316a643b8d





## 五、查询文档

#### (1) 查询所有

db.collection.find()

**实例：**

```python
# 查询所有
res = db.user.find()
# print(res) 返回结果类似一个迭代器  可以使用next方法
print(next(res))
print(next(res))
print(next(res))
print(next(res))
```

**带条件查询：**

db.collection.find({query})

**实例：**

```python
# 带条件查询
res = db.user.find({"name":"lucky"})
print(next(res))
```

#### (2) 查询一条文档

db.collection.find_one()

#### (3) 查询Id

需要导入ObjectId方法

```python
from bson.objectid import ObjectId
```

**实例：**

```python
from bson.objectid import ObjectId

# 按照Id进行查询
res = db.user.find({"_id":ObjectId("5cebda671a8f4a314762160f")})
print(next(res))
```

#### (4) 模糊查询

实例：

```python
import re
res = db.user.find({"name":re.compile("l")})
res = db.user.find({"name":{"$regex":"l"}})
print(next(res))
```



## 六、sort limit count skip的使用

#### (1) sort 排序

db.collection.find(query).sort("key",1/-1) 代表升序或者降序

**实例：**

```python
res = db.user.find().sort("age",1/-1)
# print(res)
for i in res:
    print(i)
```

#### (2) limit 取值

db.collection.find().limit(num)

**实例**

取出年龄最大的一条文档

```python
# limit
res = db.user.find().sort("age",-1).limit(1)

# print(res)
for i in res:
    print(i)
```

#### (3) count 统计

db.collection.find().count()

#### (4) skip 跳过

db.collection.find().skip(num)