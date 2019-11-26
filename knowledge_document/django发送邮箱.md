## 发送邮箱

#### 1.Django发送邮件流程分析

![image-20190830134108040](/Users/apple/qianfeng/授课/sz1903/day05/资料/day05.assets/image-20190830134108040.png)



`send_mall()`方法介绍

- 位置：
  - 在`django.core.mail`模块提供了`send_mail()`来发送邮件。
- 方法参数：
  - `send_mail(subject, message, from_email, recipient_list, html_message=None)`

```python
subject 邮件标题
message 普通邮件正文，普通字符串
from_email 发件人
recipient_list 收件人列表
html_message 多媒体邮件正文，可以是html字符串
```

#### 2.准备发邮件服务器

![image-20190830134241063](/Users/apple/qianfeng/授课/sz1903/day05/资料/day05.assets/image-20190830134241063.png)

![image-20190830134303461](/Users/apple/qianfeng/授课/sz1903/day05/资料/day05.assets/image-20190830134303461.png)

![image-20190830134329297](/Users/apple/qianfeng/授课/sz1903/day05/资料/day05.assets/image-20190830134329297.png)

![image-20190830134345418](/Users/apple/qianfeng/授课/sz1903/day05/资料/day05.assets/image-20190830134345418.png)

```python
6.配置邮件服务器

EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend' # 指定邮件后端
EMAIL_HOST = 'smtp.163.com' # 发邮件主机
EMAIL_PORT = 25 # 发邮件端口
EMAIL_HOST_USER = '290793992zb@163.com' # 授权的邮箱
EMAIL_HOST_PASSWORD = 'abc123' # 邮箱授权时获得的密码，非注册登录密码
EMAIL_FROM = 'louis<290793992zb@163.com>' # 发件人抬头


7.发送邮件
from django.core.mail import send_mail

to_email = '290793992zb@163.com'
verify_url = 'http://www.baidu.com'
subject = "显示标题"
html_message = '<p>尊敬的用户您好！</p>' \
'<p>您的邮箱为：%s 。请点击此链接激活您的邮箱：</p>' \
'<p><a href="%s">%s<a></p>' % (to_email, verify_url, verify_url)

send_mail(subject, "", settings.EMAIL_FROM, [to_email], html_message=html_message)
```

