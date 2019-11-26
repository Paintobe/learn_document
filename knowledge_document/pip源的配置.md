### windows配置

1、打开资源管理器

2、地址栏输入 `%appdata%`

3、创建文件夹`pip`，在文件夹中创建文件`pip.ini`

4、文件中写入如下内容(此处为阿里源，可自行更换源)

```
[global]
timeout = 6000
index-url = https://mirrors.aliyun.com/pypi/simple/
trusted-host = mirrors.aliyun.com
```



### linux配置

1、cd ~

2、mkdir ~/.pip

3、vim ~/.pip/pip.conf

4、输入如下内容

```
[global]
timeout = 6000
index-url = https://mirrors.aliyun.com/pypi/simple/
trusted-host = mirrors.aliyun.com
```

