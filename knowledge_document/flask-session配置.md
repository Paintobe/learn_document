#### flask-session使用

redis存储session

[文档](https://pythonhosted.org/Flask-Session/) : https://pythonhosted.org/Flask-Session/

- 安装redis   `pip install redis`

- 安装flask-session  `pip install flask-session`

- 配置文件

  ```python
  import redis
  class Config(object):
      DEBUG = True
      # session存储方式为redis
      SESSION_TYPE="redis"
      # 如果设置session的生命周期是否是会话期, 为True，则关闭浏览器session就失效
      SESSION_PERMANENT = False
      # 保存到redis的session数的名称前缀
      SESSION_KEY_PREFIX = "session:"
      # session保存数据到redis时启用的链接对象
      SESSION_REDIS = redis.Redis(host='127.0.0.1', port='6379', db=0)  # 用于连接redis的配置
  ```

- 设置session

  ```python
  from flask import session
  from flask_session import Session
  ...
  Session(app)
  ...
  @app.route('/')
  def index():
    
    session['name'] = 'lili'
    
    return 'index'
  ```

  