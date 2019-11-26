## redis主从

- ⼀个master可以拥有多个slave，⼀个slave⼜可以拥有多个slave，如此下去，形成了强⼤的多级服务器集群架构
- master用来写数据，slave用来读数据，经统计：网站的读写比率是10:1
- 通过主从配置可以实现读写分离
- ![image-20190829133722242](/Users/apple/qianfeng/授课/sz1903/day04/资料/swiper-social.assets/image-20190829133722242.png)

- master和slave都是一个redis实例(redis服务)





### 主从配置（注意：如果使用的是服务器，不要使用ipconfig的ip地址，该ip为服务器内网ip，请使用服务器的公网ip）

##### daemonize: 默认是no，表示义阻塞的方式开始服务， yes表示已后端守护进程开启



### 配置主

- 查看当前主机的ip地址    

  ```python
  ifconfig
  ```

  

- 修改etc/redis/redis.conf文件

  ```python
  sudo vi redis.conf
  bind 192.168.26.128
  ```

- 重启redis服务

  ```python
  sudo service redis stop
  redis-server redis.conf
  ```

### 配置从

- 复制etc/redis/redis.conf文件

  ```python
  sudo cp redis.conf ./slave.conf
  ```

- 修改redis/slave.conf文件

  ```python
  sudo vi slave.conf
  ```

- 编辑内容

  ```python
  bind 192.168.26.128
  slaveof 192.168.26.128 6379 # 作为哪个主服务器的从服务器
  port 6378
  ```

- redis服务

  ```python
  sudo redis-server slave.conf
  ```

- 查看主从关系

  ```python
  redis-cli -h 192.168.26.128 info Replication
  ```

### 数据操作

- 在master和slave分别执⾏info命令，查看输出信息 进入主客户端

  ```python
  redis-cli -h 192.168.26.128 -p 6379
  ```

- 进入从的客户端

  ```python
  redis-cli -h 192.168.26.128 -p 6378
  ```

- 在master上写数据

  ```python
  set aa aa
  ```

- 在slave上读数据

  ```python
  get aa
  ```




### django中配置主从

如果需要主从设置, 你需要更改 `LOCATION` 参数:

```python
"LOCATION": [
    "redis://127.0.0.1:6379/1",
    "redis://127.0.0.1:6378/1",
]
```

第一个字段代表 master 服务器, 第二个字段代表 slave 服务器.







## redis集群   （注意：如果使用的是服务器，不要使用ipconfig的ip地址，该ip为服务器内网ip，请使用服务器的公网ip）

#### 为什么要有集群

- 之前我们已经讲了主从的概念，一主可以多从，如果同时的访问量过大(1000w),主服务肯定就会挂掉，数据服务就挂掉了或者发生自然灾难
- 大公司都会有很多的服务器(华东地区、华南地区、华中地区、华北地区、西北地区、西南地区、东北地区、台港澳地区机房)

#### 集群的概念

- 集群是一组相互独立的、通过高速网络互联的计算机，它们构成了一个组，并以单一系统的模式加以管理。一个客户与集群相互作用时，集群像是一个独立的服务器。集群配置是用于提高可用性和可缩放性。当请求到来首先由负载均衡服务器处理，把请求转发到另外的一台服务器上。
- ![image-20190829231557482](redis主从和集群.assets/image-20190829231557482.png)

#### redis集群

- 分类

  - 软件层面
  - 硬件层面

- 软件层面：只有一台电脑，在这一台电脑上启动了多个redis服务。

  ![image-20190829232159306](redis主从和集群.assets/image-20190829232159306.png)

- 硬件层面：存在多台实体的电脑，每台电脑上都启动了一个redis或者多个redis服务。

  ![image-20190829232132285](redis主从和集群.assets/image-20190829232132285.png)

#### 参考阅读

- redis集群搭建 http://www.cnblogs.com/wuxl360/p/5920330.html
- [Python]搭建redis集群 http://blog.5ibc.net/p/51020.html



#### 配置机器

- 在桌面创建conf⽬录

- 在桌面创建6个redis的配置文件，文件名为7000到7005的conf配置文件

- 编辑文件，内容如下

  ```python
  port 7000  # 和文件名相同
  bind 172.16.179.130 # 本机的ip
  daemonize yes
  pidfile 7000.pid  # 和文件名相同 
  cluster-enabled yes
  cluster-config-file 7000_node.conf  # 和文件名相同 
  cluster-node-timeout 15000
  appendonly yes
  ```

- 启动redis服务

  ```python
  redis-server 7000.conf
  redis-server 7001.conf
  redis-server 7002.conf
  redis-server 7003.conf
  redis-server 7004.conf
  redis-server 7005.conf
  ```

#### 创建集群

- redis的安装包中包含了redis-trib.rb，⽤于创建集群

- 接下来的操作在172.16.179.130机器上进⾏

- 将命令复制，这样可以在任何⽬录下调⽤此命令

  ```python
  sudo cp /usr/share/doc/redis-tools/examples/redis-trib.rb /usr/local/bin/
  ```

- 安装ruby环境，因为redis-trib.rb是⽤ruby开发的

  ```python
  sudo apt-get install ruby
  ```

- 在提示信息处输⼊y，然后回⻋继续安装 

  ![image-20190829233131854](redis主从和集群.assets/image-20190829233131854-4121297.png)

- 运⾏如下命令创建集群

  ```python
  redis-trib.rb create --replicas 1 172.16.179.130:7000 172.16.179.130:7001 172.16.179.130:7002 172.16.179.131:7003 172.16.179.131:7004 172.16.179.131:7005
  ```

- 执⾏上⾯这个指令在某些机器上可能会报错,主要原因是由于安装的 ruby 不是最 新版本!

- 天朝的防⽕墙导致⽆法下载最新版本,所以需要设置 gem 的源

- 解决办法如下

  ```python
  # 先查看⾃⼰的 gem 源是什么地址
  gem source -l # 如果是https://rubygems.org/ 就需要更换
  # 更换指令为
  gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/
  # 通过 gem 安装 redis 的相关依赖
  sudo gem install redis
  # 然后重新执⾏指令
  ```

  ![image-20190829233302556](redis主从和集群.assets/image-20190829233302556-4121297.png)

  ```python
  redis-trib.rb create --replicas 1 172.16.179.130:7000 172.16.179.130:7001 172.16.179.130:7002 172.16.179.131:7003 172.16.179.131:7004 172.16.179.131:7005
  ```

- 提示如下主从信息，输⼊yes后回⻋

  ![image-20190829233430052](redis主从和集群.assets/image-20190829233430052-4121297.png)

- 提示完成，集群搭建成功

#### 数据验证

- 根据上图可以看出，当前搭建的主服务器为7000、7001、7003，对应的从服务器是7004、7005、7002

- 在172.16.179.131机器上连接7002，加参数-c表示连接到集群

  ```python
  redis-cli -h 172.16.179.131 -c -p 7002
  ```

- 写⼊数据

  ```python
  set name ben
  ```

- ⾃动跳到了7003服务器，并写⼊数据成功 

- 在7003可以获取数据，如果写入数据又重定向到7000(负载均衡) 



#### django中使用集群

```python
CACHES = {
    "default": {
        "BACKEND": "django_redis.cache.RedisCache",
        "LOCATION": "redis://127.0.0.1:6379/1",
        "OPTIONS": {
            "CLIENT_CLASS": "django_redis.client.HerdClient",
        }
    }
}
```



