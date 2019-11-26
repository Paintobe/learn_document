# MySQL数据库

## 一、MySQL数据库的介绍

##### 发展史

1996年，MySQL 1.0

2008年1月16号 Sun公司收购MySQL。

2009年4月20，Oracle收购Sun公司。


[MySQL](https://baike.baidu.com/item/MySQL/471251)是一种[开放源代码](https://baike.baidu.com/item/%E5%BC%80%E6%94%BE%E6%BA%90%E4%BB%A3%E7%A0%81)的关系型[数据库管理](https://baike.baidu.com/item/%E6%95%B0%E6%8D%AE%E5%BA%93%E7%AE%A1%E7%90%86)系统（RDBMS），使用最常用的数据库管理语言--[结构化查询语言](https://baike.baidu.com/item/%E7%BB%93%E6%9E%84%E5%8C%96%E6%9F%A5%E8%AF%A2%E8%AF%AD%E8%A8%80)（SQL）进行数据库管理。

MySQL是开放源代码的，因此任何人都可以在General Public License的许可下下载并根据个性化的需要对其进行修改。

MySQL因为其速度、可靠性和适应性而备受关注。大多数人都认为在不需要[事务](https://baike.baidu.com/item/%E4%BA%8B%E5%8A%A1)化处理的情况下，MySQL是管理内容最好的选择。

### **MySQL简介**

MySQL是一个[关系型数据库管理系统](https://baike.baidu.com/item/%E5%85%B3%E7%B3%BB%E5%9E%8B%E6%95%B0%E6%8D%AE%E5%BA%93%E7%AE%A1%E7%90%86%E7%B3%BB%E7%BB%9F/696511)，由瑞典MySQLAB 公司开发，目前属于 [Oracle](https://baike.baidu.com/item/Oracle) 旗下产品。MySQL是最流行的[关系型数据库管理系统](https://baike.baidu.com/item/%E5%85%B3%E7%B3%BB%E5%9E%8B%E6%95%B0%E6%8D%AE%E5%BA%93%E7%AE%A1%E7%90%86%E7%B3%BB%E7%BB%9F/696511)之一，在WEB 应用方面，MySQL是最好的 [RDBMS](https://baike.baidu.com/item/RDBMS/1048260) (RelationalDatabase Management System，关系数据库管理系统)应用软件MySQL所使用的SQL 语言是用于访问[数据库](https://baike.baidu.com/item/%E6%95%B0%E6%8D%AE%E5%BA%93/103728)的最常用标准化语言。MySQL软件采用了双授权政策，分为社区版和商业版，由于其体积小、速度快、总体拥有成本低，尤其是[开放源码](https://baike.baidu.com/item/%E5%BC%80%E6%94%BE%E6%BA%90%E7%A0%81/7176422)这一特点，一般中小型网站的开发都选择MySQL 作为网站数据库

### **社区版本和企业版本的区别**

主要的区别有以下两点。

1.企业版只包含稳定之后的功能，社区版包含所有Mysql的最新功能。

也就是说，社区版是企业版的测试版，但是，前者的功能要比后者多。

2.官方的支持服务只针对企业版，用户在使用社区版时出现任何问题，Mysql官方概不负责。



#### MySQL如何下载

进入MySQL官网（https://www.mysql.com）
查看底部下载-https://dev.mysql.com/downloads/mysql/



## 二、数据库的分类

#### 关系型与非关系型数据库

##### 关系型数据库的优势：

1. 复杂查询

   可以用SQL语句方便的在一个表以及多个表之间做非常复杂的数据查询

2. 事物支持

   使得对于安全性能很高的数据访问要求得以实现

##### 非关系型数据库的优势：

1. 性能

   NOSQL是基于键值对的 可以想象成表中的主键和值的对应关系 不需要经过SQL层的解析 所以性能很高

2. 可扩展性

   同样也是也因为基于键值对 数据之间没有偶尔性 所以非常容易水平扩展



## 三、主要操作

数据库表的操作 包含创建 、修改、删除、查看

数据的操作：包含增加 修改 删除 查询 简称crud

**crud:**

是指在做计算处理时的增加(Create)读取查询(Retrieve)  更新(Update)和删除(Delete) 单词首字母简写



## 四、进入到MySQL数据库

(1) 简单模式

C:\Users\xlg>mysql -uroot -p
Enter password: `******`

(2) 标准模式

 C:\Users\xlg>mysql -h127.0.0.1 -uroot -p

mysql -hlocalhost -uroot -p

mysql -h10.0.110.238 -uroot -p

Enter password: `******`



#### 参数所代表的含义：

h:host 主机（localhost IPV4 127.0.0.1）

**注意：**

root用户默认是不允许远程访问登录的 也就是IPV4的访问不了的

u:root 用户

p:password 密码

**授权root用户可以通过外网IP进行访问**

**命令：**

``` \mysql
grant all privileges on *.* to 'root'@'%' identified by 'password' with grant option
```



## 五、对于MySQL数据库的操作

##### 对于库和表操作的单词为：

创建 CREATE

删除 DROP

查看 SHOW

修改 ALTER

(1) 查看所有的数据库

show databases;

(2) 选择数据库

use 库名

(3) 查看当前库下有哪些表

show tables;

(4) 查看当前所在库

select database();

(5)创建数据库

create database 库名;

(6) 查看创建库信息

show create database 库名;

(7) 修改数据库字符编码

alter database 库名character set utf8;

(8)修改表的编码

alter table user character set utf8;

(9) 修改表中字段的字符编码

 alter table 表名modify 字段名 字段类型约束条件 character set utf8;

(10) 删除库/表
drop database 库名;

drop table 表名;

(11) 创建库并设置字符编码

create database lucky character set utf8;

(12) 创建库判断当前创建的库是否存在(防止创建库时报错)

create database if not exists lucky;

(13) 创建表判断当前创建的表是否存在(防止创建表时报错)

create table if not exists lucky(id int unsigned);

(14) 查看表结构

desc 表名;

(15) 查看创建表语句

show create table lucky;

(16) 以竖状查看 \G

show create table lucky\G

(17) 防止删除不存在的表报错

drop table if exists lucky;

(18) 防止删除不存在的库报错

drop database if exists lucky;

(19) 撤销当前命令

\c

(20) 数据库的退出

1. \q
2. exit
3. quit

#### **注意：**

1. MySQL命令以英文的分号作为结束

2. SQL命令不区分大小写

3. 在进入到一个数据库中在进入到另外一个的时候 不需要退出数据库 而是使用use再次进行数据库的切换

4. 如果创建的MySQL库编码错误的 则表和字段都为库的编码 当将库编码改为utf8 则表和字段依然没有改变 那么需要继续修改表和字段 所以在创建的时候注意库的编码

5. 更改默认创建库字符编码  

   C:\ProgramData\MySQL\MySQL Server 5.7

   64行 ：default-character-set=utf8

6. 更改不严谨报错

   sql-mode="NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION"

7. windows下表名库名不区分大小写 Linux下严格区分

8. MySQL数据库的名称具有唯一性 每个库中的表的名称也具有唯一性(库名或者一个库中的表名不要出现相同的名称)

9. 当在输入命令的时候输入完以后 添加分号不能执行命令 那么查看一下左侧是否存在引号没有闭合的情况



## 六、MySQL表的创建

### 字段类型

#### (1) 数值类型

|    类型    |             大小              |          范围(有符号)          |    范围(无符号)     |    用途     |
| :------: | :-------------------------: | :-----------------------: | :------------: | :-------: |
| tinyint  |             1字节             |        （-128,127）         |    （0,255）     |   小整数值    |
| smallint |             2字节             |      （-32768,32767）       |   （0,65535）    |   大整数值    |
|   int    |             4字节             | （-2147483648, 2147483647) | (0,4294967295) |   大整数值    |
|  float   |             4字节             |                           |                |  单精度浮点型   |
|  double  |             8字节             |                           |                |  双精度浮点型   |
| decimal  | decimal(m,d)如果m>d为m+2否则为d+2 |         依赖于m和d的值          |    依赖于m和d的值    | 小数值(更加精准) |

 **创建表语句**

```mysql
mysql> create table testnum(
    -> ttinyint tinyint,
    -> tsmallint smallint,
    -> tint int,
    -> tfloat float(6,2),
    -> tdouble double(6,2),
    -> tdecimal decimal(6,2)
    -> );
```

**创建表的主体结构：**

> create table if not exists 表名(
>
> 字段名称 字段类型 约束条件 字段说明,
>
> 字段名称 字段类型 约束条件 字段说明,
>
> ...
>
> 主键索引,
>
> 唯一索引,
>
> 常规索引
>
> )

**表插入数据语句**

**指定字段名称插入值**

insert into 表名(字段1,字段2...) values(值1,值2...)

**不指定字段插入之**

insert into 表名 values(值1,值2...)

**注意：**

1. decimal 小数类型 不仅能够保证数据计算更为精确 还可以节省空间
2. float/double/decimal 在存储的时候 小数点超出了 会四舍五入
3. 数值类型 如int /tinnyint/smallint 等 在给后面括号值的时候 没有任何的意义的 也就是说不能够去限制当前存储值的长度  除非配合约束条件zerofill 零填充的时候 才有意义




#### (2) 日期和时间类型

|    类型     | 大小(字节) |                   范围                    |         格式          |    用途    |
| :-------: | :----: | :-------------------------------------: | :-----------------: | :------: |
|   date    |   3    |          1000-01-01/9999-12-31          |     YYYY-MM-DD      |   日期值    |
|   time    |   3    |          -838:59:59/838:59:59           |      HH:MM:SS       | 时间值或持续时间 |
|   year    |   1    |                1901-2155                |        YYYY         |   年分值    |
| datetime  |   8    | 1000-01-01 00:00:00/9999-12-31 23:59:59 | YYYY:MM:DD HH:MM:SS | 混合日期和时间值 |
| timestamp |   4    |        1970-01-01 00:00:00/2038         |   YYYYMMDDHHMMSS    | 混合日期和时间值 |

**建表语句**

```mysql
mysql> create table if not exists testtime(
    -> tdate date,
    -> ttime time,
    -> tyear year,
    -> tdatetime datetime default now(),
    -> ttimestamp timestamp
    -> );
```

**日期类型注意事项：**

1. 存储日期时 我们可以使用整形类进行存储时间戳 这样做便于我们进行日期的计算
2. timestamp 值默认不为空 默认值为当前的时间戳



#### (3) 字符串类型

|          类型          |       大小       |            用途             |
| :------------------: | :------------: | :-----------------------: |
|       **char**       |    0-255字节     |           定长字符串           |
|     **varchar**      |    0-255字节     |           变长字符串           |
|       tinyblob       |    0-255字节     |     不超过255个字符的二进制字符串      |
|       tinytext       |    0-255字节     |          短文本字符串           |
|         blob         |   0-65535字节    |        二进制形式的长文本数据        |
|       **text**       |   0-65535字节    |           长文本数据           |
|      mediumblob      |  0-16777215字节  |      二进制形式的中等长度文本数据       |
|      mediumtext      |  0-16777215字节  |         中等长度文本数据          |
|       loneblob       | 0-4294697295字节 |       二进制形式的极大文本数据        |
|       lonetext       | 0-4294697295字节 |          极大文本数据           |
| **enum(成员1,成员2...)** |    65535个成员    |       枚举：可赋予某个枚举成员        |
| **set(成员1,成员2...)**  |     64个城院      | 集合：可赋予多个集合成员 多个集合成员使用逗号隔开 |

**字符串类型注意事项：**

1) char和varchar的区别

+ char执行效率高于varchar （但占用空间大）
+ varchar相对于char节省空间
+ char和varchar 类型的长度范围都在0-255之间
+ 当给char类型传入值的长度低于给定的长度 则为使用空格填充到指定长度
+ varchar类型传入的值小于给定的长度 不会使用空格填充
+ 如果开启了不严谨报错 给定的值超出了设定的长度 会自动截取

2) enum和set的区别

+ enum只能选择多个成员中的一个成员

+ set可以选择多个成员 如果存在重复的成员则会自动去重

+ enum和set都只能选择给定成员


3） blob和text类型

+ blob和text类型都是可以存放任意大数据的数据类型
+ blob区分大小写 text不区分大小写




**创建表语句**

```mysql
mysql> create table if not exists teststr(
    -> tchar char(11),
    -> tvarchar varchar(5),
    -> ttext text,
    -> tenum enum('w','m'),
    -> tset set('1','2','3','4')
    -> );
```

**插入数据**

```mysql
insert into teststr values(15611833906,123,'我是内容','w',1);
```



## 七、字段约束

1. unsigned 无符号 只能存储正数

   只能用于设置数值类型 不允许出现负数 

   最大存储长度会增加一倍

   **实例：**

   ```mysql 
   mysql> create table testcon(
       -> age1 tinyint,
       -> age2 tinyint unsigned
       -> );
   insert into testcon(age1,age2) values(255,255);
   ```

   **注意：**

   如果开启了不严谨报错 会按照当前存储最大值近些截取 如果设置了无符号 不允许插入负值的

2. zerofill  零填充

   只能用于设置数值类型 在数值之前会自动用零补齐不足的位数

   **实例：**

   ```mysql
   alter table testcon add zv int(5) zerofill; 修改表testcon添加子弹zv类型int 约束为零填充
   insert into testcon(zv) values(1234);
   >>> 01234 #补位1个
   ```

3. auto_increment 自增

   用于设置字段的自动增长 每增加一条记录 该字段的值会自动增加

   **实例：**

   ```mysql
   mysql> create table autoincre(
       -> id int primary key auto_increment,
       -> username varchar(20)
       -> );
   ```

   **注意：**

   自增需要配合索引去使用

   插入数值的时候 无需给值 自动增长 步长默认为1

4. default 默认值

   可以通过此属性来指定一个默认值  如果没有在此列添加值 那么默认值为当前添加的值  如果不给default默认值 则默认值为null 如果给当前存在默认值的字段时 当前字段值为你给定的值

   **实例：**

   ```mysql
   alter table autoincre add sex enum('w','m') default 'w';
   insert into autoincre(username) values('lucky');
   ```

5. null 和 not null

   字段没有给定默认值的情况下 值默认为null  如果给当前字段指定了not null 则必须在插入值的时候 给not null 的字段插入值

   **实例：**

   ```mysql
   alter table user add age tinyint unsigned not null;
   ```

6. comment  设置说明

   **实例：**

   ```mysql
   在创建的使用设置说明
   mysql> create table testcom(
       -> info varchar(40) comment '存储个人信息字段'
       -> );
   修改字段的说明
   alter table user modify username varchar(20) comment '存储用户名'
   设置表的说明信息
   alter table 表名 comment='说明内容'
   ```




## 八、null值注意事项

(1) null值意味着没有值或未知值

(2) 不能对null值进行算数运算

(3) 对null值进行算数运算 其结果还是null

(4) 0或者null 都意味着假 其余值都为真



## 九、MySQL的索引

#### MySQL主要有四种索引

主键索引 primary key

唯一索引 unique

常规索引 index

全文索引 fulltext



#### (1) 主键索引

主键索引是关系数据库中最常见的索引类型 主要作用是确定数据表里一条特定的数据记录的位置 

我们可以在字段后添加primary key 来对字段设置为主键索引

**注意事项**

1. 最好为每张表指定一个主键 但不是必须指定
2. 一个表只能指定一个主键 而且主键的值不能为空 通常和auto_increment 搭配

**创建**

```mysql 
create testprim(
id int unsigned primary key auto_increment
)
```



##### 自增得步长

mysql的默认步长是居于会话session的 查看全局变量 其中默认为1

查看步长

show session variables like 'auto_inc%';

设置步长 只能针对当前的会话

set session auto_incrment_increment = 2; 设置会话步长为2

查看全局

show global variables liek 'auto_inc%';

修改全局级别的

set global auto_increment_increment = 1;

##### 修改自增值（自增归位）

1. alter table user auto_increment = 1;
2. truncate 表名 (清空表 并将自增归位)

#### (2) 常规索引 index

常规索引技术是关系型数据库查询中最重要的技术 如果要提升数据库的性能 索引优化是首先应该考虑的 因为它能使我们的数据库得到最大性能方面的提升  

**缺点：**

1. 多占用磁盘空间
2. 会减慢插入 删除 和 修改的操作

**创建常规索引：**

创建常规索引 可以使用 index 和 key 关键字随表一同创建

**实例：**

```mysql 
mysql> create table testindex(
    -> username varchar(20),
    -> index luckyindex(username)
    -> );
mysql> create table testkey(
    -> username varchar(20),
    -> key (username)
    -> );
```

**说明：**

给username字段设置一个常规索引 索引名称为luckyindex 

如果不给所以字段起名称 默认索引名称为字段名

**注意：**

1. 在给mysql创建常规索引和唯一索引的时候 单独一行去创建  不要和字段放在一行 出错！
2. 一个表中可以存在多个常规索引 但是要根据具体的情况去设置 某个字段有大量的查询的时候



#### (4) 唯一索引

唯一索引与主键索引一样 都可以防止创建重复的值  但是 不同之处在于 每个数据表中只能有一个主键索引 但是可以有多个唯一索引 使用unique对字段 定义唯一索引

**注意：**

如果在给表中字段插入值的情况报错 查看 字段是否设置了唯一索引

**创建**

```mysql 
mysql> create table testunique(
    -> username varchar(20),
    -> email varchar(50),
    -> phone char(11),
    -> unique(username),
    -> unique uniemail(email),
    -> unique(phone)
    -> );
```

**说明：**

给usernam email phone设置了唯一索引  其中email设置了索引名称为uniemail 其余索引名称为 默认字段名

#### (5) 全文索引

全文索引在mysql中是一个fulltext类型索引 但fulltext索引只能用于MyISAM表  并且只可以在char varchar 或text类型的字段上创建  

**缺点：**

fulltext是不支持中文全文索引的

**创建**

```mysql
 CREATE TABLE `textfull` (
  `article` text,
  FULLTEXT KEY `article` (`article`)
) ENGINE=MyISAM DEFAULT CHARSET=utf8
```

alter table 表名 add fulltext(字段名称)



## 十 数据表类型与存储位置

MyISAM和InnoDB俩种类型最为重要

MyISAM和InnoDB的区别

1. MyISAM表类型的数据表会产生三个文件 InnoDB产生二个文件
2. MyISAM 表类型的数据表效率更高
3. innodb的安全性高于MyISAM 
4. innodb支持事物处理  MyISAM不支持
5. innodb支持外键  ，MyISAM不支持



**MyISAM存储表文件的作用：**

MyISAM与innodb共有的文件 .frm:存储数据表的框架结构 文件名与表名是相同的  每个表对应一个同名的frm文件 

.MYD: my data 表数据文件

.MYI: my index 索引文件



**InnoDB 存储表文件的作用：**

.ibd:存放数据库表数据和索引 



数据库：

数据库也是以文件形式存储在磁盘上  Data文件中





## 十一、innodb的事物处理

如果MySQL的配置文件没有更改过  那么默认为MyISAM 可以在my.ini配置文件中 更改为innodb

也可以通过命令去更改：

> alter table 表名 engine = innodb/myisam



(1) 查询当前是否为 自动提交 

select  @@autocommit 

如果值为1 则为自动提交 

(2) 开启事物处理

set autocommit = 0

(3) 事物开始

begin

(4) 执行SQL语句

insert into user values(null,'lucky','w',18)

(5) 提交或回滚

commit work;

rollback work;

**注意：**

1. 如果开启了事物 在处理数据后 没有进行提交或回滚 那么你的操作和没操作一样 也就是相当于回滚了 
2. 只有innodb支持事物处理  MyISAM不支持



## 十二、建表的注意事项

1. 表的字段之间要使用逗号隔开  最后一个字段不要存在逗号
2. 数据表名不要和字段名重名
3. auto_increment 属性 必须依赖于主键索引
4. 表名称和字段名称 尽量不要使用MySQL系统的关键字
5. 使用反引号 会使创建的表效率增高



## 十三、对表结构的操作

1. 给表添加一个新的字段

   alter table 表名 add 字段名 类型 约束条件 说明

   alter table user add info varchar(50) not null default '我是帅气的lucky老师啊';

2. 删除一个字段

   alter table 表名drop 字段名

   alter table user drop age;

3. 更改字段名

   alter table  表名 change 原字段名  新字段名 字段类型 约束条件 说明

   alter table user change info userinfo varchar(50) not null default '我是帅气的lucky老师啊';

4. 修改字段信息

   alter table 表名 modify 字段名 字段类型 约束条件 说明

    alter table user modify sex tinyint unsigned not null default 1;

5. 给字段改变位置 

   alter table  表名 modify 字段名 字段类型 约束条件  first   第一位

   + alter table user modify sex varchar(20) not null default 1 first;

   alter table  表名 modify 字段名 字段类型 约束条件  after 字段名称   当前字段放在某个字段的后面

   + alter table user modify sex tinyint not null default 1 after id;

6. 表添加索引

   alter table 表名 add 索引类型 索引名称(字段名)   添加索引名

   + alter table user add key si(sex);
   + alter table user add unique su(sex);

   alter table 表名 add 索引类型(字段名)   不添加索引名

   + alter table user add key(username);
   + alter table user add unique(username);

7. 删除索引

   alter table 表名 drop key 索引名;

   alter table user drop key username_2;

8. 创建一个和a表一样表结构的b表

   create table b like  a;

9. 修改表和字段的字符编码

   alter table 表名 character set utf8;

   alter table 表名 modify 字段名 类型 约束条件 character set utf8;

   ​

## 十四、INSERT 数据的添加

1. 指定字段添加值

   insert into 表名(字段1,字段2....) values(值1,值2...)

   insert into user(sex,username) values(0,'lucky');

2. 不指定字段添加值

   insert into 表名 values(值1,值2...)

   insert into user values(null,0,'lucky','我是lucky老师');

3. 指定字段添加多个值

   insert into 表名(字段1,字段2....) values(值1,值2...),(值1,值2...)...

   insert into user(sex,username) values(1,'苍苍'),(0,'蒹葭');

4. 不指定字段添加多个值

   insert into 表名 values(值1,值2...),(值1,值2...)...

    insert into user values(null,1,'xxx','xxx'),(null,0,'xxl','xxl');

**注意事项：**
指定字段与不指定字段在添加值的时候 按照从左至右依次对应给值





## 十五、SELECT查询

1. 不指定字段的查询（不建议）

   select * from 表名

2. 指定字段的数据查询(建议)

   select 字段名1,字段名2... from  表名

   select  username,userinfo from user;

3. 对查询的字段起别名

   select username as u from user;

   select username  u from user;

4. 给查询的结果添加一个新字段

   select username u,'北京' as address from user;

   select num1+num2 as total from num;



## 十六、UPDATE修改

1. 修改一个字段的值

   update 表名 set 字段名=值;

   update user set username='帅气的lucky' where id = 3;

2. 修改多个字段的值

   update 表名 set 字段名1=值1,字段名2=值2...;

   update user set sex=0,userinfo='xxx的个人简介' where id=7;

3. 给字段的值在原有的基础上改变值

    update user set sex=sex+2;



**注意：**

在进行数据的修改的时候 一定记得给定where条件  如果没有给定where条件 则修改的为整张表当前字段的值



## 十七、DELETE 删除

**主体结构：**

```mysql
delete from 表名 [where ...]
```

**实例：**

delete from user; 删除user表中所有的数据 

**注意：**

删除 一定注意添加 where 条件   否则会删除整张表中的数据  并且auto_increment自增所记录的值不会改变  所以需要将自增归位

**自增归位：**

1. alter tabe 表名 auto_increment = 1
2. truncate 表名; 清空表数据 并将自增归位



## 十八、WHERE条件

**实例表结构：**

+----------+-------------+------+-----+-----------------------+----------------+
| Field    | Type        | Null | Key | Default               | Extra          |
+----------+-------------+------+-----+-----------------------+----------------+
| id       | int(11)     | NO   | PRI | NULL                  | auto_increment |
| sex      | tinyint(4)  | NO   |     | 1                     |                |
| username | varchar(20) | YES  |     | NULL                  |                |
| age      | tinyint(4)  | NO   |     | 18                    |                |
| userinfo | varchar(50) | NO   |     | 我是帅气的lucky老师啊 |                |
+----------+-------------+------+-----+-----------------------+----------------+

#### (1) 比较运算符

1. `>`

   将id大于5 的性别 更改为0 年龄改为20岁

   update user set sex=0,age=20 where id>5;

2. `<`

   将id小于3 的性别 更改为0 年龄改为23岁

   update user set sex=0,age=23 where id<3;

   查看id小于4的 性别和用户名的字段数据

   select sex,username from user where id<4;

3. `>=`

   删除 id大于等于6的数据

   delete from user where id>=6;

4. `<=`

   查询年龄小于等于23的数据

   select * from user where age<=23;

5. =

   查询性别为0的数据

   select * from user where sex=0;

6. `!=/<>`

   查询 用户名不等于lucky的所有数据

   select * from user where username!='lucky';

   select * from user where username<>'lucky';

#### (2) 逻辑运算符

1. and 逻辑与 俩侧为真结果为真

   查询年龄在18到23之间 不包括本身

   select * from user where age>18 and age<23;

   修改年龄为30 id大于1 小于等于2

   update user set age=30 where id>1 and id<=2;

2. or 逻辑或运算 俩侧条件满足一侧就可以

   select * from user where age=10 or age=30;

   select * from user where age>=10 or age<=30;

3. between and 在...范围之内 包括本身

   查询年龄在18~20之间的所有数据

   select * from user where age between 18 and 20;

   等同于

   select * from user where age>=18 and age<=20;

4. not between and 不在...之间

   查询年龄不在18~20之间的所有数据

   select * from user where age not between 18 and 20;

   等同于

   select * from user where age<18 or age>20;

5. in 在...里

   查询 年龄在18,20的数据

   select * from user where age in(18,20);

   等同于

   select  * from user where age=18 or age=20;

6. not in 不在...里

   查询 年龄在18,20的数据

   select * from user where age not in(18,20);

   等同于

   select  * from user where age!=18 and age!=20;

   ​

#### (三) order by 排序  升序/降序

   升序

   查询数据 按照年龄升序（默认）

   select * from user order by age;

   select * from user order by age asc;

   查询数据 按照年龄降序

   select * from user order by age desc;

#### (4) limit 取值

**结构：**

limit x 取出x条数据

limit x,y 从x的位置取出y条数据

取出3条数据

 select * from user limit 3;

取出年龄最大/最小的一条数据

select * from user order by age desc limit 1;

select * from user order by age limit 1;

从0开始取出3条数据

select * from user limit 3; 等同于 select * from user limit 0,3;

**分页实例：**

数据一共100条

每页10条数据

第一页   limit  0,10

第二页   limit   10,10

第三页   limit   20,10

**公式：**

(nowpage-1)*10



#### (5) is/is not 查询为null的数据

查询username为null的数据

select * from user where username is null;

查询username不为null的数据

select * from user where username is not null;

**注意：**

因为null是特殊的值  所有不能使用 = 或者 !=进行查询



#### (6) like 模糊查询

1. ’%字符‘ 查询以字符结尾的数据

   查询以三字为结束的username的数据

   select * from user where username like '%三';

2. '字符%' 查询以字符开头的数据

   select * from user where username like '赵%';

3. '%字符%' 查询包含字符的数据

   查询 userinfo中包含lucky的数据

   select * from user where userinfo like '%lucky%';

4. '\_' 通配符_ 代表匹配任意一个字符

   查询 用户名一个字符的数据

   select * from user where username like '_' 

   查询_lucky的数据 第一位为任意字符

   select * from user where username like '_ucky' 

5. not like 

   查询 用户名除了俩个字符以外的任意数据

   select * from user where username not like '__';

6. [charlist] 原子表  原子表内的任意一个字

   从上面的 "Persons" 表中选取居住的城市以 "A" 或 "L" 或 "N" 开头的人：

   ```
   SELECT * FROM Persons
   WHERE City LIKE '[ALN]%'
   ```


#### (7) DISTINCT 去除重复的数据

select distinct 字段名  from 表名;

 select distinct userinfo from user;

#### (8) 子查询 (查询的条件还是一条SQL语句)

select  * from 表名 where 字段名 in(SQL语句)

**实例：**

select * from user where age in(select age from user where sex=0);

## 十九、 聚合函数

1. count 统计个数
2. max 最大值
3. min 最小值
4. sun 求和
5. avg 求平均数

select count(*) as count,max(age),min(age),avg(age),sum(age) from user;

## 二十、 group by 分组

主体结构 

select count(字段) from 表名 group by 字段

统计 男生和女生分别有多少人

select sex,count(*) from user group by sex;

统计每班有多少人

select class,count(*) from user group by class;

统计 每班的男生和女生分别有多少人

select class,sex,count(*) as count from user group by class,sex;

**having** 分组的条件的使用 相当于 where

查询人数大于2人的班级

select class,count(*) as count from user group by class having count>2;

查询班级为 3班和4班的人数

select class,count(*) as count from user group by class having class in('onlin3','onlin4');

查询班级为3班和4班的人数 并且人数大于2人

select class,count(*) as count from user group by class having class in('onlin3','onlin4') and count >2;





## 二十一、多表联查

**表结构：**

 user表

+----------+-------------+------+-----+-----------------------+----------------+
| Field    | Type        | Null | Key | Default               | Extra          |
+----------+-------------+------+-----+-----------------------+----------------+
| id       | int(11)     | NO   | PRI | NULL                  | auto_increment |
| sex      | tinyint(4)  | NO   |     | 1                     |                |
| username | varchar(20) | YES  |     | NULL                  |                |
| age      | tinyint(4)  | NO   |     | 18                    |                |
| userinfo | varchar(50) | NO   |     | 我是帅气的lucky老师啊 |                |
| class    | varchar(20) | NO   |     | onlin4                |                |
+----------+-------------+------+-----+-----------------------+----------------+

adddress表

+---------+------------------+------+-----+---------+----------------+
| Field   | Type             | Null | Key | Default | Extra          |
+---------+------------------+------+-----+---------+----------------+
| id      | int(10) unsigned | NO   | PRI | NULL    | auto_increment |
| uid     | int(11)          | NO   |     | NULL    |                |
| address | varchar(255)     | NO   |     | NULL    |                |
| code    | varchar(255)     | NO   |     | NULL    |                |
+---------+------------------+------+-----+---------+----------------+

#### (1) 隐式内连接

**主体结构：**

select * from 表名1,表名2... where 表名1.字段名=表名2.字段名 and ...

查询id为1的用户名和地址

```mysql
SELECT
	*
FROM
	USER,
	address
WHERE
	`user`.id = address.uid
AND `user`.id = 1
```

获取某个字段的值和起别名

```mysql
SELECT
	u.username,a.address
FROM
	USER u,
	address a
WHERE
	u.id = a.uid
AND u.id = 1
```



#### (2) 显示内连接 inner join

**主体结构：**

select * from 表1 inner join 表2 on 条件;

查询id为1的用户名和地址

**实例：**

```mysql
SELECT
	u.username,a.address
FROM
	USER u inner join
	address a
on
	u.id = a.uid
AND u.id = 1
```



#### (3) 左连接 left join

**主体结构：**

select * from 表1 left join 表2 on 条件;

查询id为1的用户名和地址

**实例：**

```mysql
SELECT
	u.username,a.address
FROM
	USER u left join
	address a
on
	u.id = a.uid
```



#### (4) 右连接 right join

**主体结构：**

select * from 表1 left join 表2 on 条件;

查询id为1的用户名和地址

**实例：**

```mysql
SELECT
	u.username,a.address
FROM
	USER u right join
	address a
on
	u.id = a.uid
```



**注意：**

1. 显示内连接和隐示内连接是相同的  会将俩端匹配的数据查询出来  
2. 左连接 会以左表为主表 右表为辅表 将主表的数据全部查询出来  辅表的数据没有的用null来占位
3. 右连接 会以右表为主表 左表为辅表 将主表的数据全部查询出来  辅表的数据没有的用null来占位



## 二十二、其它操作

#### (1) 修改密码

set password for 用户名@localhost=password('用户名');

#### (2) 创建其它用户分配权限

1. 使用MySQL库

   use mysql

2. 查看当前库下有哪些用户

   select user from user;

3. 创建用户

   create user 用户名 identified by '密码'

   create user lucky identified by '123456';

4. 赋予权限

   grant all on lucky.* to 用户名

   all权限代表增删查 

   grant insert,select on lucky.* to lucky;

5. 回收权限

   revoke all on lucky.* from lucky;

6. 修改用户名

   rename user lucky to zhangsan;

7. 删除用户

   drop user zhangsan;

8. 刷新

   flush privileges



## 二十三、触发器

**概述：**

触发器：它是一个特殊的存储过程   他是MySQL在 insert update delete 的时候执行 自动执行  不能直接调用

它包含四个要素

1. 监事地点(table)
2. 监事时间(insert/update/delete)
3. 触发时间(after/before)
4. 触发时间(insert/update/delete)

**主体结构：**

```python
create trigger trigger_name
after/before insert/update/delete on table_name
for each row
begin
sql 语句(触发的语句一句或多句)
end;
```

创建俩张表 商品表goods和订单表order 来说明触发器的使用实例

表结构：

goods表

+------------+------------------+------+-----+---------+----------------+

| Field | Type | Null | Key  | Default | Extra |
| ----- | ---- | ---- | ---- | ------- | ----- |
|       |      |      |      |         |       |

+------------+------------------+------+-----+---------+----------------+
| goods_id   | int(10) unsigned | NO   | PRI | NULL    | auto_increment |
| goods_name | varchar(255)     | NO   |     | NULL    |                |
| goods_num  | int(11)          | NO   |     | NULL    |                |
+------------+------------------+------+-----+---------+----------------+

order表

```mysql
+-----------+------------------+------+-----+---------+----------------+
| Field     | Type             | Null | Key | Default | Extra          |
+-----------+------------------+------+-----+---------+----------------+
| order_id  | int(10) unsigned | NO   | PRI | NULL    | auto_increment |
| goods_id  | int(11)          | YES  |     | NULL    |                |
| order_num | int(11)          | YES  |     | NULL    |                |
+-----------+------------------+------+-----+---------+----------------+
```

将goods表添加四条数据

insert into goods(goods_name,goods_num) values('手机',20),('电脑',30),('单反',20);

(1) 实现购买任意商品  对应的商品数量响应的减少

分析：

监事地点：order表

监事事件: insert 操作

触发时间：insert之后

触发事件：update操作

**实例：**

```mysql
create trigger t1
after insert on `order`
for each row
begin
update goods set goods_num=goods_num-new.order_num where goods_id=new.goods_id;
end;
```

**注意：**

new代表新增的一行的数据 行中每一列的值用new.列名来表示

(2) 购买5个手机

insert into `order`(goods_id,order_num) values(1,5);

再去查询会发现商品的数量发生了更改 自动减少

(3) 撤销订单

分析：

监事地点： order表

监视事件：delete操作

出发时间 : 在delete 操作之后

触发事件:update 操作

```mysql
drop trigger if exists t1;
create trigger t1
after delete on `order`
for each row
begin
update goods set goods_num=goods_num+old.order_num where goods_id=old.goods_id;
end;
```

取消刚才买的5个手机的订单

delete from `order` where order_id=1;

当删除以后会发现  商品的数量将删除的订单的数量进行累加



## 二十四、Python操作MySQL

**安装：**

pip install pymysql;

**使用：**
import pymysql

#### (1) 链接MySQL数据库

db  = pymysql.connect(主机名,用户名,密码,数据库名)

#### (2) 设置字符集

db.set_charset('utf8')

#### (3) 创建游标对象

cursor = db.cursor()

#### (4) 执行SQL语句

cursor.execute(sql语句)

#### (5) 获取结果集

获取所有

cursor.fetch_all()

获取一条

cursor.fetch_one()

#### (6) 获取受影响的行数

cursor.rowcount

#### (7) 关闭数据库连接

db.close()

**事物：**

pymysql默认开启了事物处理 所以在添加数据的时候 需要commit 或者rollback

**实例：**

```python
try:
    sql = 'insert into user values(null,1,"曹操",100,"曹操第一奸雄","魏国")'
    print(sql)
    cursor.execute(sql)
    db.rollback()
except:
    db.commit()
```

### 实例 登录注册

**表结构**

```mysql
+----------+------------------+------+-----+---------+----------------+
| Field    | Type             | Null | Key | Default | Extra          |
+----------+------------------+------+-----+---------+----------------+
| id       | int(10) unsigned | NO   | PRI | NULL    | auto_increment |
| username | char(11)         | NO   | UNI | NULL    |                |
| password | varchar(12)      | NO   |     | NULL    |                |
+----------+------------------+------+-----+---------+----------------+
```

**MD5加密**

```python
import hashlib


def md5(str):
    m = hashlib.md5()
    m.update(str.encode("utf8"))
    print(m.hexdigest())
```

**实例：**

```python
import pymysql,re


class LR:
    # 当进行类的实例化的时候 会自动调用 把一些作为类需要初始化的代码 进行操作
    def __init__(self,host='127.0.0.1',user='root',password='123456',db='test'):
        # 连接mysql数据库 选择test数据库
        self.db = pymysql.connect(host,user,password,db)
        # 设置字符集
        self.db.set_charset('utf8')
        # 创建游标对象
        self.cursor = self.db.cursor()

    # 注册
    def register(self):
        username = input('请输入手机号码')
        password = input('请输入密码(6~12位)')
        # 正则匹配数据是否正确
        usernameRes = re.match('1[3-9][0-9]{9}$',username)
        passwordRes = re.match('\w{6,12}',password)
        # 这里的return 目前的作用是 阻止代码不再向下继续执行
        if not usernameRes:
            print('请输入正确的手机号码')
            return
        if not passwordRes:
            print('请输入正确的密码')
            return

        # 当上面的数据都没有任何问题 则进行查询该用户名是否存在
        sql = 'select id from user where username="{}"'.format(username)
        # 执行sql语句
        self.cursor.execute(sql)

        # 查询当前结果受影响的行数
        if self.cursor.rowcount:
            print('该用户名已存在')
            return
        # 异常处理  有问题则回滚  没有问题则提交
        try:
            # 插入数据
            sql = 'insert into user(username,password) values("{}","{}")'.format(username,password)
            self.cursor.execute(sql)
            self.db.commit()
            print('恭喜：%s 注册成功'%username)
        except:
            self.db.rollback()
            print('注册失败 当前系统繁忙')

    # 登录
    def login(self):
        username = input('请输入手机号码')
        password = input('请输入密码(6~12位)')
        # 正则匹配数据是否正确
        usernameRes = re.match('1[3-9][0-9]{9}$', username)
        passwordRes = re.match('\w{6,12}', password)
        # 这里的return 目前的作用是 阻止代码不再向下继续执行
        if not usernameRes:
            print('请输入正确的手机号码')
            return
        if not passwordRes:
            print('请输入正确的密码')
            return

        # 查询该用户名是否存在
        sql = 'select username,password from user where username="{}"'.format(username)
        self.cursor.execute(sql)
        if not self.cursor.rowcount:
            print('请输入正确的用户名')
            return

        # 该用户存在 取出数据
        data = self.cursor.fetchone()
        if username == data[0] and password == data[1]:
            print('登录成功 欢迎：',username)
            return
        print('请输入正确的用户名和密码')



lr = LR()
# lr.register()
lr.login()
```

**优化登录注册类**

```python
import pymysql,re


class LR:
    # 当进行类的实例化的时候 会自动调用 把一些作为类需要初始化的代码 进行操作
    def __init__(self,host='127.0.0.1',user='root',password='123456',db='test'):
        # 连接mysql数据库 选择test数据库
        self.db = pymysql.connect(host,user,password,db)
        # 设置字符集
        self.db.set_charset('utf8')
        # 创建游标对象
        self.cursor = self.db.cursor()

    # 封装公共的方法
    def publicFunc(self):
        self.username = input('请输入手机号码')
        self.password = input('请输入密码(6~12位)')
        # 正则匹配数据是否正确
        usernameRes = re.match('1[3-9][0-9]{9}$', self.username)
        passwordRes = re.match('\w{6,12}', self.password)
        # 这里的return 目前的作用是 阻止代码不再向下继续执行
        if not usernameRes:
            print('请输入正确的手机号码')
            return False
        if not passwordRes:
            print('请输入正确的密码')
            return False
            # 当上面的数据都没有任何问题 则进行查询该用户名是否存在
        sql = 'select username,password from user where username="{}"'.format(self.username)
        # 执行sql语句
        self.cursor.execute(sql)
        return True

    # 注册
    def register(self):
        # 调用公共的方法去进行判断
        if not self.publicFunc():
            return

        # 查询当前结果受影响的行数
        if self.cursor.rowcount:
            print('该用户名已存在')
            return
        # 异常处理  有问题则回滚  没有问题则提交
        try:
            # 插入数据
            sql = 'insert into user(username,password) values("{}","{}")'.format(self.username,self.password)
            self.cursor.execute(sql)
            self.db.commit()
            print('恭喜：%s 注册成功'%self.username)
        except:
            self.db.rollback()
            print('注册失败 当前系统繁忙')

    # 登录
    def login(self):
        # 调用公共的方法去进行判断
        if not self.publicFunc():
            return

        if not self.cursor.rowcount:
            print('请输入正确的用户名')
            return

        # 该用户存在 取出数据
        data = self.cursor.fetchone()
        if self.username == data[0] and self.password == data[1]:
            print('登录成功 欢迎：',self.username)
            return
        print('请输入正确的用户名和密码')



lr = LR()
lr.login()
```