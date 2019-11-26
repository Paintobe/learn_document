#### flask中发送邮件

- 安装 flask-mail    `pip install flask-mail`

- 配置邮箱的参数

  ```python
  class Config:
      ...
      MAIL_SERVER = 'smtp.163.com' # 默认163的服务器
      MAIL_PORT = 25
      MAIL_USERNAME = 'shuliming98@163.com' # 邮箱名称
      MAIL_PASSWORD = '******' # 客户端授权密码  需要去163查找授权密码
  ```

- 在 ext.py文件中延迟加载mail

  ```python
  from flask_mail import Mail
  
  ...
  mail = Mail()
  
  def load_ext(app):
  
      ...
      mail.init_app(app)
  
  ```

- 创建发送邮件的函数app/utils/func.py中创建

  ```python
  from flask_mail import Message
  from app.config import Config
  from app.ext import mail
  
  def send_email(to_email):
  
      msg = Message("激活邮件",
                    sender=Config.MAIL_USERNAME,
                    recipients=[to_email])
  
      msg.body = ""
      msg.html = "<b>testing</b>"
  
      mail.send(msg)
  ```

