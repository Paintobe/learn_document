#### flask中celery的使用

安装celery 和 redis 

`pip install cellery`      `pip install redis`



1 在app/config.py中，配置

```python
class Config:
    CELERY_BROKER_URL = 'redis://localhost:6379/2'
    CELERY_RESULT_BACKEND = 'redis://localhost:6379/2'
    CELERY_TASK_SERIALIZER = 'json'
```



2 app/`__init__`.py中

```python
from celery import Celery
from app.config import Config

celery = Celery(__name__, broker=Config.CELERY_BROKER_URL)

def create_app():
    app = Flask(__name__)
    # ....
    celery.conf.update(app.config)	# 更新 celery 的配置
    # ...
    return app
```



3 在方法文件中

```python
from app import celery

@celery.task
def send_mail(to_email):
  pass
```



4 执行方法

```python
send_mail.delay(to_email)
```



5 在manage.py同级目录下创建celery_worker.py

```python
from app import create_app, celery

app = create_app()
app.app_context().push()
```



6 运行

```python 
celery worker -A celery_worker.celery -l info
```

