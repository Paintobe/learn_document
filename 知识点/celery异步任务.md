#### Celery 及异步任务的处理

1. 模块组成

   ![celery](E:\Qianfeng train\note\stage5\day02\资料\swiper01.assets\celery.png)

   - 任务模块 Task

     包含异步任务和定时任务. 其中, 异步任务通常在业务逻辑中被触发并发往任务队列, 而定时任务由 Celery Beat 进程周期性地将任务发往任务队列.

   - 消息中间件 Broker

     Broker, 即为任务调度队列, 接收任务生产者发来的消息（即任务）, 将任务存入队列. Celery 本身不提供队列服务, 官方推荐使用 RabbitMQ 和 Redis 等.

   - 任务执行单元 Worker

     Worker 是执行任务的处理单元, 它实时监控消息队列, 获取队列中调度的任务, 并执行它.

   - 任务结果存储 Backend

     Backend 用于存储任务的执行结果, 以供查询. 同消息中间件一样, 存储也可使用 RabbitMQ, Redis 和 MongoDB 等.

2. 安装

   ```
   pip install celery
   ```

3. 创建实例

   ```python
   import time
   from celery import Celery

   broker = 'redis://127.0.0.1:6379'
   backend = 'redis://127.0.0.1:6379/0'
   app = Celery('my_task', broker=broker, backend=backend)

   @app.task
   def add(x, y):
       time.sleep(5)     # 模拟耗时操作
       return x + y
   ```

4. 启动 Worker

   ```
   celery worker -A tasks --loglevel=info
   ```

5. 调用任务

   ```python
   from tasks import add

   add.delay(2, 8)
   ```

6. 常规配置

   ```python
   broker_url = 'redis://127.0.0.1:6379/0'
   broker_pool_limit = 1000  # Borker 连接池, 默认是10

   timezone = 'Asia/Shanghai'
   accept_content = ['pickle', 'json']

   task_serializer = 'pickle'
   result_expires = 3600  # 任务过期时间

   result_backend = 'redis://127.0.0.1:6379/0'
   result_serializer = 'pickle'
   result_cache_max = 10000  # 任务结果最大缓存数量

   worker_redirect_stdouts_level = 'INFO'
   ```

7. 在django环境中执行celery

   ```python
   import os

   from celery import Celery

   from worker import config

   # 加载django的环境
   os.environ.setdefault("DJANGO_SETTINGS_MODULE", "django_swiper.settings")

   # 实例化celery
   celery_app = Celery('swiper')

   # 加载配置文件
   celery_app.config_from_object(config)

   # 自动注册任务
   celery_app.autodiscover_tasks()

   ```

8.celery异步发送短信实例

- 安装celery和django-redis

- 在根目录创建一个worker的包

- 在包的`__init__`实例化celery对象

  ```python
  import os

  from celery import Celery

  from worker import config

  # 加载django的环境
  os.environ.setdefault("DJANGO_SETTINGS_MODULE", "swiper.settings")  #这里的swiper与项目主目录名字一致

  # 实例化celery
  celery_app = Celery('swiper')   #名字任意取

  # 加载配置文件
  celery_app.config_from_object(config)

  # 自动注册任务
  celery_app.autodiscover_tasks()

  ```

- 创建一个配置文件config.py，存放celery的配置

  ```python
  broker_url = 'redis://127.0.0.1:6379/0'
  ```

- 在封装的异步函数里面用户celery来装饰这个函数

  ```python
  from worker import celery_app

  @celery_app.task
  def send_sms_celery(phone):
    pass
  ```

- 把任务放到异步的celery里面执行

  ```python
  send_sms_celery.delay(phone)
  ```

- 启动celery

  ```python
  celery worker -A worker -l info
  ```

  ​