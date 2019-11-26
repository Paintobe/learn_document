#### 上线配置

##### 修改settings配置

```python
DEBUG = False
ALLOWED_HOSTS = ['*']
```



##### 收集项目静态文件

当Django运行在**生产环境**时，将**不再提供静态文件的支持**，需要将**静态文件交给静态文件服务器**。

我们需要收集项目中静态文件，并放到静态文件服务器中。

我们使用Nginx服务器作为静态文件服务器。

1. 收集项目静态文件

   1. 配置收集静态文件存放的目录

      ```python
      STATIC_ROOT = os.path.join(os.path.dirname(BASE_DIR), 'static')
      ```

   2. 执行收集静态文件命令

      ```python
      python manage.py collectstatic
      ```

2. 部署Nginx服务器提供静态数据

   1. 在指定的目录新建配置文件`axf.conf`

   2. 配置如下

      ```python
      server { 
              listen       80;
              server_name  www.axf.cn;
              location /static {
                  alias /Users/apple/Desktop/demo/static;
              }
      }
      ```

   3. 修改`/etc/hosts` 文件, 新增如下配置     window:  windows/system32/drivers/etc/hosts

      ```shell
      127.0.0.1  www.axf.cn
      ```

   4. 启动Nginx服务器

      ```shell
      # 检查配置文件
      $ sudo /usr/local/nginx/sbin/nginx -t
      # 首次启动
      $ sudo /usr/local/nginx/sbin/nginx
      # 重启
      $ sudo /usr/local/nginx/sbin/nginx -s reload
      # 停止
      $ sudo /usr/local/nginx/sbin/nginx -s stop
      ```

      





#### uWSGI服务器配置

1. 安装uwsgi包

   ```python
   pip install uwsgi
   ```

2. 准备uwsgi服务器配置文件, 在根目录创建 uwsgi.ini

   ```python
   [uwsgi]
   # 使用Nginx连接时使用，Django程序所在服务器地址
   socket=127.0.0.1:9999
   # 直接做web服务器使用，Django程序所在服务器地址
   # http=127.0.0.1:9999
   # 项目目录
   chdir=/Users/apple/Desktop/demo/axf_1905
   # 项目中wsgi.py文件的目录，相对于项目目录
   wsgi-file=axf_1905/wsgi.py
   # 进程数
   processes=4
   # 线程数
   threads=2
   # uwsgi服务器的角色
   master=True
   # 存放进程编号的文件
   pidfile=uwsgi.pid
   # 日志文件
   daemonize=uwsgi.log
   # 虚拟环境路径
   virtualenv=/Users/apple/Envs/axf_1905
   
   ```

3. 管理`uwsgi服务器`

   ```python
   # 启动
   $ uwsgi --ini uwsgi.ini
   # 关闭
   $ uwsgi --stop uwsgi.pid
   ```





#### 部署Nginx服务器反向代理

1. 修改Nginx服务器配置文件

```shell
server {
        listen       80;
        server_name  www.axf.cn;
        ......
        location / {
        		uwsgi_pass 127.0.0.1:9999;
            include uwsgi_params;
        }

    }
```

2. 启动Nginx服务器

   ```shell
   # 检查配置文件
   $ sudo /usr/local/nginx/sbin/nginx -t
   # 重启
   sudo /usr/local/nginx/sbin/nginx -s reload
   ```

   