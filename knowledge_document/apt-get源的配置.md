### ubuntu下apt-get源配置

1、备份原文件

`sudo mv /etc/apt/sources.list /etc/apt/sources.list.bak`

后缀为`.bak`的为备份文件，以防配置错误或不想更换apt源，将此文件改回原名即可

2、编辑apt源文件

`sudo vim /etc/apt/sources.list`

3、将内存全部替换，替换如下内容

下列配置为ubuntu16.04 LTS的配置

如需其他版本或下列源无效，可去`<https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/>`

自行拷贝相应的ubuntu版本或最新的apt源（此为清华大学源，如需其他源，可自行查找替换即可，步骤一致）

```
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-security main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ xenial-security main restricted universe multiverse
```

4、更新源

sudo apt-get update  或 sudo apt update