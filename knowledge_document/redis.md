# Redis数据库

## 一、前期准备

设置redis.windows.conf

455行   maxheap 1024000000 设置最大的数据堆的大小

387行  requirepass   123456  设置数据库的密码

**端口号**

6379



## 二、启动服务

cd redis的目录中

**实例：**

C:\Users\xlg>cd C:\redis64-2.8.2101

C:\redis64-2.8.2101>redis-server  redis.windows.conf

服务一直运行  没有结束  证明服务开启成功



## 三、测试是否连接成功

打开一个新的终端

输入密码  这个密码就是在redis.windows.conf文件中添加的 requirepass的密码

C:\Users\xlg>cd C:\redis64-2.8.2101

C:\redis64-2.8.2101>redis-cli
127.0.0.1:6379> auth 123456
OK
127.0.0.1:6379> keys *



## 四、redis简介

redis是完全开源免费的  遵守BSD协议  是一个高性能的key-value数据库

redis与其它key-value缓存产品有以下的特点：

redis支持数据的持久化 可以将内存中的数据保存在磁盘中  重启的时候可以再次加载进行使用

redis不仅仅支持简单的key-value类型的数据 ,同时还提供list set zset hash等数据结构的存储

redis:半持久化  存储与内存和硬盘中



## 五、redis和mongodb的区别

redis是完全在内存中保存数据的数据库  使用磁盘只是为了持久性 redis数据全部存在内存   定期写入磁盘 当内存不够时 可以选择指定的lru算法删除数据

mongodb是文档型的非关系型数据库  mongodb更类似mysql  支持字段索引   游标操作  其优势在于查询功能比较强大  擅长查询json数据  能够存储海量数据   但是不支持事物



## 六、Redis值的类型

1. 字符串  string
2. 哈希 hash
3. 列表   list
4. 集合 set
5. 有序集合 zset

数据库操作的全部命令：
http://redis.cn/commands.html



### (1) String 字符串

**概述：**

string是reids的最基本的类型 最大能存储 512M的数据 string类型是二进制的  可以存储任何数据  比如数字  图片 序列化对象等

一个key 对应一个value

#### 1.设置键值

A、设置键值  

> set key value

set  name lucky

B、设置键值及过期时间 以秒为单位

> setex key seconds value

setex age 10 18

C、查看有效时间 以秒为单位

> ttl key

ttl age

D、只有在key不存在时设置key的值

> setnx key value

setnx name test

E、设置多个键值

> mset key value [key value...]

mset name lucky age 18....



#### 2.key的操作

A、根据键获取值  如果键不存在 则返回None(null 0 nil)

> get key

get name

B 获取多个key的值

> mget key1 [key2 ...]

mget name age sex

C 返回key中 字符串值的子字符

> getrange key start end

getrange name 0 2

D 将给定的值 设为value  并返回旧值

> getset key value

getset name test



#### 3.运算

要求： 值是字符串类型的数字

A 将key的值+1

> incr key

incr age

B 将key对应的值-1

> decr key

decr age

C 将key对应的值+整数

> incrby key intnum 

incrby age 5

D 将key对应的值 - 整数

> decrby key intnum

decrby age 5



#### 4.其它

A 追加值

> append key value

append age 20

B 获取长度

> strlen key 

strlen age



## key 键的操作

A 查询所有符合给定模式pattern（正则表达式）的key

> keys *
>
> keys \*o*
>
> keys t??

**支持正则表达式的模式：**

+ h?llo 匹配hello hallo 或者hbllo
+ h*llo 匹配 hllo haaaaallo
+ h[ef]llo 匹配 hello hfllo
+ h[\^e]llo 匹配 第二位除了e以外
+ h[a-z]llo 匹配第二位为a-b的任意小写字母

**实例：**

keys h?llo

keys h*llo

keys h[a-b]llo

B 判断键key是否存在  

> exists key

exists name

C 查看key对应的 value的类型

> type key

type name

D 删除键及对应的值

> del key [key...]

del name age

E 设置过期时间 以秒为单位

> expire key seconds

expire name 10

F 查看有效时间 秒为单位

>  ttl key

ttl name

G 查看有效时间 毫秒为单位

> pttl key

pttl name

H 移除key的过期时间 将key持久保持

> persist key

persist name

I 删除所有的key

> flushdb  删除当前数据库中所有的key
>
> flushall 删除所有数据库中的 key

J 修改key的名称 当新的key名不存在时

> renamenx key newkey

renamenx name age

K 重命名

> rename key newkey

rename name age

L 将key移动到指定的数据库中

> move key db

move name 1将name的key value 移动到1库中

M 随机返回一个key

> randomkey



### (2) hash 哈希

**概述：**

hash用于存储对象

{

​	name:lucky,

​	age:18

}

redis hash 是一个键值对的集合

#### 1 设置

A 设置单个值

> hset key field value

hset myset name lucky

B 设置多个值

> hmset key field value [field value...]

hmset myset a a b b c c 

C 为哈希表key中指定的字段的整数值上增量increment

> hincrby myset key increment

hincrby myset  age 10

D 只有在字段field不存在时 设置哈希表字段的值

> hsetnx key field value

hsetnx myset name lucky 

#### 2 获取

A  获取一个属性的值

> hget key value

hget myset name

B 获取多个属性的值

> hmget key field [filed...]

hmget myset name age sex

C 获取所有字段和值

> hgetall key

hgetall myset

D 获取所有的字段

> hkeys key

hkeys myset

E 获取所有的值

> hvals key

hvals myset

F 返回包含数据的个数

> hlen key

hlne myset 

#### 3 其它

A 判断字段是否存在  存在返回1 否则返回0

> hexists key field

hexists myset name

B 删除字段及值

> hdel key field [field...]

hdel myset name age sex

C 返回值的字符串长度

> hstrlen key field 起始版本3.2.0



### (3) 列表 list

**概述：**

reids列表是简单的字符串列表  按照插入顺序 进行排序  你可以添加一个元素到列表的头部(左边) 或者尾部(右边)

头部[a,b,c,d]尾部

#### 1 设置

A 在头部插入

> lpush key value [value...]

lpush mylist 1 2 3

B 将一个值插入到已存在的列表头部  列表不存在时 操作无效

> lpushx key value

lpushx myilst 4

C 在一个元素的前|后插入新元素

>  linsert key before | after value value

linsert mylist after 1 5

D 在尾部插入

> rpush key  value [value]

rpush mylist  6 7 8

E 为已存在的列表添加值

> rpushx key value 

rpushx mylist 9

F 更改索引所对应的值

> lset key index value

lset mylist 0 1  将索引0对应的值更改为1



#### 2 获取

A 移除并返回key对应的list的第一个元素

> lpop key

lpop mylist

B 移除并返回 key对应的list的最后一个元素

> rpop key

rpop mylist

C 返回存储在key的列表中指定范围的元素

> lrange key start end

lrange mylist 0 -1 获取mylist列表的所有元素

**注意：**
索引从0开始  -1代表最后一个元素



#### 3 其它

A 裁剪列表 改为原集合的一个子集

> ltrim key stvart end

ltrim mylist 1 -1

B 返回存储在key里的list的长度

> llen key

llen mylist

C 返回列表中索引对应的值

> lindex key index

lindex mylist 0



### (4) 集合 set

**概述：**

无序集合 元素类型为string类型  元素具有唯一性  不重复

{a,b}

#### 1 设置

A 添加元素

> sadd key member member...

sadd myset a b c d

#### 2 获取

A 返回key 集合中所有元素

> smembers key

smembers myset

B 返回集合元素个数

> scard key

scard myset

C 移除并返回集合中的一个随机元素

> spop key

spop myset

D 返回集合中一个或多个随机数

> srandmember key [count]

srandmember myset 返回一个随机元素

srandmember myset  2  返回俩个随机元素

E 移除集合中一个或多个成员

> srem key member [member...]

srem myset a b c d

#### 3 集合的其它操作

A 求多个集合的交集

> sinter key key ...

sinter set1 set2

B 求多个集合的差集

> sdiff key key ...

sdiff set1 set2  # 注意比较顺序

C 求多个集合的合集

> sunion key key ...

sunion set1 set2

D 判断元素是否在集合中  存在返回1  不存在 返回0

> sismember key member

sismember set1 a



### (5) 有序集合 zset

**概述：**

1. 有序集合  元素类型为String  元素具有唯一性  不能重复
2. 每个元素都会关联一个score(表示权重) 通过权重的大小进行排序  元素的score 是可以相同的

#### 1 设置

A 添加

> zadd key score member [score member...]

zadd myzset 1 a 2 c 3 b

B 有序集合中对指定成员 的分数上增加增量increment

> zincrby key increment member

zincrby myzset 1 a



#### 2 获取

A 返回指定范围的元素

> zrange key start end

zrange myzset 0 -1

B 返回元素个数

> zcard key

zcard myzset

C 返回有序集合key中  score在min和max之间的元素的个数

> zcount key min max

zount myzset 1 3

D 返回有序集合中 成员member的score值

> zscore key member

zscore myzset a



**其它**

在我们进入数据以后 默认存在0库中 可以通过select 数据库编号(0-15) 进行切换 这些编号的数据库都是固定的



## 七、持久化设置

### RDB 和 AOF

RDB：RDB方式按照一定的时间间隔 对数据集创建基于时间的快照

DOF：AOF方式记录server收到写的操作到日志文件   在server重启的时候 通过回访这些操作来重建数据集 

#### (1) RDB持久化设置

默认情况下 redis在磁盘上创建二进制格式的命名为dump.rdb的数据快照 可以通过配置文件 配置每个N秒且数据集上至少有M个变化时创建快照 是否对数据进行压缩  快照名称  存放快照的工作目录  redis的默认配置如下

```
900秒后且至少一个key发生变化时创建快照
save 900 1
300秒后且至少10个key发生变化时创建快照
save 300 10
60秒收 且至少10000个key发生变化时创建快照
save 60 10000
创建快照时 对数据进行压缩
rdbcompression yes
快照名称
dbfilename dump.rdb
```

#### (2) AOF持久化设置

利用快照的持久化方式不是非常可靠  当运行redis的计算机 停止工作  意外断电  意外杀掉了redis的进程  那么最近写入redis的数据将会丢失  AOF方式是一个替代的方案  用以最大限度的持久化数据  通过配置redis.conf进行开启还是关闭

```
关闭aof
appendonly no
开启aof
appendonly yes
```

