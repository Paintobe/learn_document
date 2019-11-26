### 配置redis做django缓存

- 安装 `pip install django-redis`

- settings 配置

  ```python
  CACHES = {
      "default": {
          "BACKEND": "django_redis.cache.RedisCache",
          "LOCATION": "redis://127.0.0.1:6379/0",
          "OPTIONS": {
              "CLIENT_CLASS": "django_redis.client.DefaultClient",
              "PICKLE_VERSION": -1,
          }
      }，
      "session": {
          "BACKEND": "django_redis.cache.RedisCache",
          "LOCATION": "redis://127.0.0.1:6379/2",
          "OPTIONS": {
              "CLIENT_CLASS": "django_redis.client.DefaultClient",
              "PICKLE_VERSION": -1,
          }
      }
  }
  ```


- 指定session的保存方案

  ```python
  SESSION_ENGINE = "django.contrib.sessions.backends.cache"
  SESSION_CACHE_ALIAS = "session"
  ```

