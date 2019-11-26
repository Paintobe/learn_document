# Python操作redis

安装：

pip install redis

**导入：**

import redis

#### 连接方式

1. StrictRedis 实现大部分官方的命令
2. Redis 是StrictRedis的子类  用于向后兼容旧版本的redis

官方推荐使用StrictRedis

**连接实例**

```python
import redis
redis.Redis(host='127.0.0.1',password="密码",port=6379,db=0,decode_responses=True)
r = redis.StrictRedis(host='127.0.0.1',decode_responses=True)
print(r)
```

**decode_responses=True 获得的结果自动进行解码  否则不填加次参数  手动解码 res.decode('utf-8')**

#### 连接池 connection pool



**概述：**

管理一个redis server的所有连接  避免每次建立  释放连接的开销  默认 每个redis实例 都会维护一个自己的连接池 可以直接建立一个连接池  作为参数传递给redis  这样可以实现多个redis共享一个连接池

**实例：**

```python
pool = redis.ConnectionPool(host='127.0.0.1',db=0,port=6379,decode_responses=True)
r = redis.Redis(connection_pool=pool)
print(r)
```



## 一、python操作字符串类型

**连接**

```python
import redis
r = redis.Redis(host='127.0.0.1',db=0,decode_responses=True)
```



(1) set 设置值 set

```python
# set 设置值
r.set('name','lucky')
```

(2) 获取值 get

```python
# 获取值
print(r.get('name'))
```

(3) 批量设置值mset

```python
# 批量设置值
# r.mset(age=18,sex='男',hobby="写代码")
```

(4) 批量获取值 mget

```python
print(r.mget('name','age','sex','hobby'))
```

(5)设置新值  打印原值 getset

```
print(r.getset('name','张三'))
```

(6) 返回对应值的长度 strlen

```python
print(r.strlen('hobby'))
```

(7) 追加值 append

```
# 追加值
r.append('age',1)
print(r.get('age'))
```

(8) 查看类型 type

```python
print(r.type('name'))
```



## 二、python操作hash类型

(1) 设置 hset

```python
# hset 设置
r.hset('myset','name','lucky')
```

(2) 获取 hget

```python
# 获取值
print(r.hget('myset','name'))
```

(3) 获取所有键值  hgetall

```python
# 获取所有键值
print(r.hgetall('myset'))
```

(4) 批量设置键值对  hmset

```python
# 批量设置键值对
r.hmset('mset',{'name':'张三','age':20})
```

(5) 批量获取多个key的值 hmget

```python
# 量获取多个key的值
print(r.hmget('mset',['name','age']))
```

(6)  获取hash中键值对的个数 hlen

```python
# hlen 获取键值对的个数
print(r.hlen('mset'))
```

(7) 获取hash中所有的key值 hkeys

```python
# 获取hash中所有的key值
print(r.hkeys('mset'))
```

(8) 获取hash中所有的value值 hvals

```python
# 获取所有的value值
print(r.hvals('mset'))
```

(9) 检查当前的hash中是否有当前的key hexists

```python
# 判断key是否存在
print(r.hexists('mset','name'))
```

(10) 删除hash指定的key hdel

```python
# 删除key
r.hdel('mset','name')
```



## 三、List操作

(1) lpush 从头部添加元素

```python
# 头部添加元素
r.lpush('list',1,2,3,4)
```

(2) rpush 从尾部添加元素

```python
# 从尾部添加元素
r.rpush('list',5,6)
```

(3) llen 获取元素的个数

```python
# 获取元素的个数
print(r.llen('list'))
```

(4) linsert 在列表的某个值的前后插入一个新值

```python
# 在列表的前后插入新值
r.linsert('list','after',5,7)
```

参数1 name key值

参数2 前后 before/after

参数3 在某个元素的前后插入

参数4 插入的值

(5) lrem 删除list中指定的值

```python
# 删除元素
r.lrem('list',7)
```

(6) lpop  移除列表最左侧的一个元素 并返回

```python
# 移除第一个元素
print(r.lpop('list'))
```

(7) lindex 根据索引获取列表的元素

```python
# 通过索引获取元素
print(r.lindex('list',0))
```

(8) lrange 分片获取元素

```python
# 切片获取元素
print(r.lrange('list',0,-1))
```



## 四、python操作Set类型

(1) sadd 给name对应的集合添加元素

```python
# 添加元素
r.sadd('set','a','b','c')
```

(2) smembers 获取集合中的所有元素

```python
# 获取集合中的所有元素
print(r.smembers('set'))
```

(3) scard 后去name对应的集合中元素的个数

```python
# 获取元素的个数
print(r.scard('set'))
```

(4) sdiff 多个集合的差集

```python
# sdiff
print(r.sdiff('set','set2'))
```

(5) sinter 获取并集

```python
# 获取并集
print(r.sinter('set','set2'))
```

(6) sismember 检查当前的值是否是当前集合内的元素

```python
# 检查元素是否存在
print(r.sismember('set','a'))
```

(7) spop 从集合的右侧删除一个元素

```python
# 右侧删除元素并返回
print(r.spop('set'))
```



## 五、python操作zset有序集合类型

(1) zadd 添加元素

```python
# 添加元素
r.zadd('zset',a=1,b=2,c=3)
```

(2) zcard 获取有序集合内元素的数量

```python
# 获取集合内元素的数量
print(r.zcard('zset'))
```

(3) zcount 获取有序集合中 权重在min和max之间的个数

```python
# zcount 获取权重之间的个数
print(r.zcount('zset',1,2))
```

(4) zrange 返回一个范围内的元素

```python
# 返回一个范围内的元素
print(r.zrange('zset',0,-1))
```

(5) zscore 获取元素所对应的权重

```python
# 获取value对应的权重
print(r.zscore('zset','c'))
```

