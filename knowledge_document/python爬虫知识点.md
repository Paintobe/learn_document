### http 协议

1、http请求

​	包含：请求行、请求头、请求内容

2、常见请求头：

```
accept:浏览器通过这个头告诉服务器，它所支持的数据类型
Accept-Charset: 浏览器通过这个头告诉服务器，它支持哪种字符集
Accept-Encoding：浏览器通过这个头告诉服务器，支持的压缩格式
Accept-Language：浏览器通过这个头告诉服务器，它的语言环境
Host：浏览器通过这个头告诉服务器，想访问哪台主机
If-Modified-Since: 浏览器通过这个头告诉服务器，缓存数据的时间
Referer：浏览器通过这个头告诉服务器，客户机是哪个页面来的  防盗链
Connection：浏览器通过这个头告诉服务器，请求完后是断开链接还是何持链接
X-Requested-With: XMLHttpRequest  代表通过ajax方式进行访问
```

3、响应头：

```
Location: 服务器通过这个头，来告诉浏览器跳到哪里
Server：服务器通过这个头，告诉浏览器服务器的型号
Content-Encoding：服务器通过这个头，告诉浏览器，数据的压缩格式
Content-Length: 服务器通过这个头，告诉浏览器回送数据的长度
Content-Language: 服务器通过这个头，告诉浏览器语言环境
Content-Type：服务器通过这个头，告诉浏览器回送数据的类型
Refresh：服务器通过这个头，告诉浏览器定时刷新
Content-Disposition: 服务器通过这个头，告诉浏览器以下载方式打数据
Transfer-Encoding：服务器通过这个头，告诉浏览器数据是以分块方式回送的
Expires: -1  控制浏览器不要缓存
Cache-Control: no-cache  
Pragma: no-cache
```

### urllib库基本使用

Python2：urllib  urllib2

Python3: urllib.request   urllib.parse

```
urllib.request
	urlopen(url)   发送请求
	urlretrieve(url, image_path)  下载
urllib.parse
	quote   url编码函数，将中文进行转化为%xxx
	unquote url解码函数，将%xxx转化为指定字符
	urlencode  给一个字典，将字典拼接为query_string,并且实现了编码的功能
response
	read()       读取相应内容，内容是字节类型
	geturl()     获取请求的url
	getheaders() 获取头部信息，列表里面有元组
	getcode()    获取状态码
	readlines()  按行读取，返回列表，都是字节类型
```

### urllib携带cookie登录

```
# 创建一个cookiejar对象
cj = http.cookiejar.CookieJar()
# 通过cookiejar创建一个handler
handler = urllib.request.HTTPCookieProcessor(cj)
# 根据handler创建一个opener
opener = urllib.request.build_opener(handler)
往下所有的操作都是用opener.open方法去发送请求，因为这里面携带cookie
```

### 正则解析

**详细正则可查看正则.md文件**

```
单字符：
	. : 除换行以外所有字符
	[] ：[aoe] [a-w]匹配集合中任意一个字符
	\d ：数字  [0-9]
    \D : 非数字
    \w ：数字、字母、下划线、中文
    \W : 非\w
    \s ：所有的空白字符
    \S : 非空白
数量修饰：
    * : 任意多次  >=0
    + : 至少1次   >=1
    ? : 可有可无  0次或者1次
    {m} ：固定m次
    {m,} ：至少m次
    {m,n} ：m-n次
边界：
    \b \B 
    $ : 以某某结尾 
    ^ : 以某某开头
分组：
    (ab){3}
    (){4}  视为一个整体
    ()     子模式\组模式   \1  \2
贪婪模式
	.*?  .+?
re.I : 忽略大小写
re.M ：多行匹配
re.S ：单行匹配
match\search\findall
re.sub(正则表达式, 替换内容, 字符串)
```

### bs4解析

```
BeautifulSoup
需要安装：pip install bs4
    bs4在使用时候需要一个第三方库，把这个库也安装一下
    pip install lxml
简单使用：
    说明：选择器，jquery
    from bs4 import BeautifulSoup
    使用方式：可以将一个html文档，转化为指定的对象，然后通过对象的方法或者属性去查找指定的内容
    	（1）转化本地文件：
			soup = BeautifulSoup(open('本地文件'), 'lxml')
		（2）转化网络文件：
			soup = BeautifulSoup('字符串类型或者字节类型', 'lxml')
	（1）根据标签名查找
		soup.a   只能找到第一个符合要求的标签
	（2）获取属性
		soup.a.attrs  获取所有的属性和值，返回一个字典
		soup.a.attrs['href']   获取href属性
		soup.a['href']   也可简写为这种形式
	（3）获取内容
		soup.a.string
		soup.a.text
		soup.a.get_text()
		如果标签还有标签，那么string获取到的结果为None，而其它两个，可以获取文本内容
	（4）find
		soup.find('a')   找到第一个符号要求的a
		soup.find('a', title="xxx")
		soup.find('a', alt="xxx")
		soup.find('a', class_="xxx")
		soup.find('a', id="xxx")
		find方法不仅soup可以调用，普通的div对象也能调用，会去指定的div里面去查找符合要求的节点
		find找到的都是第一个符合要求的标签
	（5）find_all
		soup.find_all('a')
		soup.find_all(['a', 'b'])
		soup.find_all('a', limit=2)  限制前两个
	（6）select
		根据选择器选择指定的内容
		常见的选择器：标签选择器、类选择器、id选择器、组合选择器、层级选择器、伪类选择器、属性选择器
		a  
		.dudu
		#lala
		a, .dudu, #lala, .meme
		div .dudu #lala .meme .xixi  下面好多级
		div > p > a > .lala   只能是下面一级
		input[name='lala']
		select选择器返回永远是列表，需要通过下标提取指定的对象，然后获取属性和节点
		该方法也可以通过普通对象调用，找到都是这个对象下面符合要求的所有节点
```

### xpath解析

```
pip install lxml
	什么是xpath？
		xml是用来存储和传输数据使用的
		和html的不同有两点：
		（1）html用来显示数据，xml是用来传输数据
		（2）html标签是固定的，xml标签是自定义的
		xpath用来在xml中查找指定的元素，它是一种路径表达式
		常用的路径表达式
		// : 不考虑位置的查找
		./ : 从当前节点开始往下查找
		@ : 选取属性
实例：
    /bookstore/book  选取根节点bookstore下面所有直接子节点book
    //book           选取所有book
    bookstore//book  查找bookstore下面所有的book
    /bookstore/book[1]  bookstore里面的第一个book
    /bookstore/book[last()]  bookstore里面的最后一个book
    /bookstore/book[position()<3]  前两个book
    //title[@lang]    所有的带有lang属性的title节点
    //title[@lang='eng']  所有的lang属性值为eng的title节点任何元素节点
属性定位
	//input[@id="kw"]
	//input[@class="bg s_btn"]
层级定位
索引定位
	//div[@id="head"]/div/div[2]/a[@class="toindex"]
	【注】索引从1开始
	//div[@id="head"]//a[@class="toindex"]
	【注】双斜杠代表下面所有的a节点，不管位置
逻辑运算
	//input[@class="s_ipt" and @name="wd"]
模糊匹配
	contains
		//input[contains(@class, "s_i")]
		所有的input，有class属性，并且属性中带有s_i的节点
		//input[contains(text(), "爱")]
	starts-with
		//input[starts-with(@class, "s")]
		所有的input，有class属性，并且属性以s开头取文本
	//div[@id="u1"]/a[5]/text()  获取节点内容
	//div[@id="u1"]//text()      获取节点里面不带标签的所有内容直接将所有的内容拼接起来返回给你
	ret = tree.xpath('//div[@class="song"]')
	string = ret[0].xpath('string(.)')
	print(string.replace('\n', '').replace('\t', ''))
取属性
	//div[@id="u1"]/a[5]/@href
代码中使用xpath
	from lxml import etree
	两种方式使用：将html文档变成一个对象，然后调用对象的方法去查找指定的节点
	（1）本地文件
		tree = etree.parse(文件名)
	（2）网络文件
		tree = etree.HTML(网页字符串)
	ret = tree.xpath(路径表达式)
	【注】ret是一个列表
```

### jsonpath解析

```
jsonpath: 用来解析json数据使用的
	Python处理json格式用到的函数
		import json
		json.dumps() : 将字典或者列表转化为json格式的字符串
		json.loads() ：将json格式字符串转化为python对象
		json.dump() : 将字典或者列表转化为json格式字符串并且写入到文件中
		json.load() ：从文件中读取json格式字符串，转化为python对象
	前端处理：
		将json格式字符串转化为js对象
		JSON.parse('json格式字符串')
		eval('(' + json格式字符串 + ')')
	安装：
		pip install lxml
		pip install jsonpath
	http://blog.csdn.net/luxideyao/article/details/77802389
	xpath和jsonpath的对比
		/     $   根元素
		.     @   当前元素
		/     .   子元素
		//    ..  任意位置查找
		*     *   通配符
		[]    ?() 过滤
		xpath 索引下标从1开始
		jsonpath 索引下标从0开始
```

### selenium和PhantomJS

```
selenium是什么？
	是一个Python的一个第三方库，对外提供的接口可以操作你的浏览器，然后浏览器完成自动化的操作
PhantomJS是什么？
	是一款浏览器，是无界面浏览器
使用selenium
	安装：pip install selenium
操作谷歌浏览器，首先必须有谷歌浏览器的一个驱动
谷歌驱动下载地址
		http://chromedriver.storage.googleapis.com/index.html
谷歌驱动和谷歌浏览器版本关系映射表
	http://blog.csdn.net/huilan_same/article/details/51896672
代码操作
	from selenium import webdriver
	browser = webdriver.Chrome(path)
	browser.get()
使用下面的方法，查找指定的元素进行操作即可
	find_element_by_id         根据id找节点
	find_elements_by_name      根据name找
	find_elements_by_xpath     根据xpath查找
	find_elements_by_tag_name  根据标签名找
	find_elements_by_class_name  根据class名字查找
	find_elements_by_css_selector  根据选择器查找
	find_elements_by_link_text   根据链接内容查找
get\send_keys\click
```

### Headless Chrome

```
引入无界面谷歌浏览器
	因为phantomjs现在都不维护了
	mac、linux，版本号在59+以上，才支持这种模式
	windows，要求版本号在60+以上，才支持这种模式
	from selenium.webdriver.chrome.options import Options
	chrome_options = Options()
	chrome_options.add_argument('--headless')
	chrome_options.add_argument('--disable-gpu')
```

### requests的使用

```
安装：pip install requests
官方文档：
	http://cn.python-requests.org/zh_CN/latest/
用来做什么？
	和urllib是同一个位置的
get请求
定制头部
	data：是一个原生字典即可
	requests.get(url, headers=headers, params=data)
响应对象
	r.text  字符串形式查看响应
	r.content 字节类型查看响应
	r.encoding 查看或者设置编码类型
	r.status_code 查看状态码
	r.headers  查看响应头部
	r.url      查看所请求的url
	r.json()   查看json格式数据
post请求
	formdata: 是一个原生字典即可
	r = requests.post(url=url, headers=headers, data=formdata)
ajax、get、post
	和上面的是一样的
代理
	r = requests.get(url, headers=headers, proxies=proxies)
```

### requests的cookie登录

```
s = requests.session()
	s.post()
	s.get()
用此方式发起请求，自动携带cookie
```

### tesseract

​	有兴趣可以了解

### scrapy框架的使用

```
1、scrapy是什么？
	是Python的一个爬虫框架，非常出名、非常强悍，你是框架，学的就是用法，当然，底层肯定使用了多进程、多线程、队列等技术
安装：pip install scrapy
框架的介绍
	框架有5部分组成
	引擎、下载器、spiders、调度器（schedule）、管道（pipeline）
	我们的代码写到spiders、管道中，spiders里面我们要实现文件内容解析，链接提取，管道：数据是保存到文件中、mysql中、MongoDB中？
简单使用：
	（1）创建项目
		scrapy startproject firstblood
	（2）认识目录结构
		firstblood
			firstblood           真正的项目文件
				pycache      缓存文件
				spiders          爬虫文件存放的地方
					pycache
					init.py
					lala.py      爬虫文件（*）
				init.py      包的标志
				items.py         定义数据结构的地方（*）
				middlewares.py   中间件
				pipelines.py     管道文件（*）
				settings.py      配置文件（*）
			scrapy.cfg           不用管
	（3）生成爬虫文件
		cd firstblood
		scrapy    genspider    爬虫名称     网址域名(如www.xxx.com)
		name: 爬虫名字
		allowed_domains: 允许的域名
		start_urls: 起始url
		parse: 自动回调的解析内容函数
	（4）认识response对象
		程序跑起来：
			cd firstblood/firstblood/spiders
			scrapy crawl 爬虫名称
			(问题1)pywin32安装一下，注意版本
			(问题2)取消遵从robots协议
				settings.py中第22行
			(问题3)修改UA头部信息
				settings.py中第19行
		response的常用方法和属性
			text: 字符串类型
			body: 字节类型
			xpath(): scrapy内部已经集成了xpath，直接使用即可，此xpath非彼xpath，略有不同
	（5）执行输出指定格式
		scrapy crawl qiubai -o qiubai.json
		scrapy crawl qiubai -o qiubai.xml
		scrapy crawl qiubai -o qiubai.csv
2、scrapy shell
	response属性、方法
	selector对象
	item对象
3、yield item和请求
```

### crawlspider的使用

```
crawlspider是什么？
	也是一个spider，是Spider的一个子类，所以其功能要比Spider要强大
	多的一个功能是：提取链接的功能，根据一定的规则，提取指定的链接
（1）.创建scrapy工程：scrapy startproject projectName
（2）.创建爬虫文件：scrapy genspider -t crawl spiderName www.xxx.com
链接提取器
	LinkExtractor(
		allow=xxx,   # 正则表达式，要（*）
		deny=xxx,    # 正则表达式，不要这个
		restrict_xpaths=xxx,  # xpath路径（*）
		restrict_css=xxx, # 选择器（*）
		deny_domains=xxx, # 不允许的域名
	)
用法演示
	scrapy shell http://www.xxxx.com/movie/(爬取的起始网站链接)
	from scrapy.linkextractors import  LinkExtractor
	通过正则提取链接
		links = LinkExtractor(allow=r'/movie/\?page=\d')
	将所有包含这个正则表达式的href全部获取到返回
		links.extract_links(response)进行查看提取到的链接
		【注】将重复的url去除掉
	通过xpath提取
		links = LinkExtractor(restrict_xpaths='//ul[@class="pagination pagination-sm"]/li/a')
	通过css提取
		links = LinkExtractor(restrict_css='.pagination > li > a')
使用
	调度器有去重的功能，只要包含了，就可以爬取所有页面
```

### 分布式爬虫

```
1、存储到mysql、mongodb
	通过crawlspider经常爬取这些有分页、有详情页的
	读取settings文件中的参数:
		from scrapy.utils.project import get_project_settings
		settings = get_project_settings()
	custom_settings
		# 自己定制配置文件中的某些选项
	    custom_settings = {
	        "ITEM_PIPELINES": {
	            'movieproject.pipelines.MyMongoDbPipeline': 302,
	        }
	    }
2、redis简单回顾
	配置
	windows redis启动
		redis-server.exe redis.windows.conf
	linux redis客户端连接windows的服务器
		redis-cli -h 10.8.153.5
	配置windows的redis服务器可以让其它客户端连接和读写
		第56行，把这个注释掉
			#bind 127.0.0.1
		第75行
			protected-mode no
3、分布式部署
	scrapy ： 一个框架，不能实现分布式爬取
	scrapy-redis ： 基于这个框架开发的一套组件，可以让scrapy实现分布式的爬取
	（1）安装： pip install scrapy-redis
	（2）样本查看
		https://github.com/rmax/scrapy-redis
		example-project\example\spiders
		dmoz.py : 普通crawlspider，没有参考价值
		myspider_redis.py ： 分布式的Spider模板
		mycrawler_redis.py ： 分布式的CrawlSpider模板
		Spider       ====》  RedisSpider
		CrawlSpider  ====》  RedisCrawlSpider
		name                 name
		redis_key            start_urls
		init()           allowed_domains
		【注】init()是一个坑，现在还是使用allowed_domains这种列表的形式
	（3）存储到redis中
		scrapy-redis组件已经写好往redis中存放的管道，只需要使用即可，默认存储到本机的redis服务中
		如果想存储到其它的redis服务中，需要在配置文件中配置
		REDIS_HOST = 'ip地址'
		REDIS_PORT = 6379
	（4）部署分布式
		爬虫文件按照模板文件修改
		配置文件中添加
			# 使用scrapy-redis组件的去重队列
			DUPEFILTER_CLASS = "scrapy_redis.dupefilter.RFPDupeFilter"
			# 使用scrapy-redis组件自己的调度器
			SCHEDULER = "scrapy_redis.scheduler.Scheduler"
			# 是否允许暂停
			SCHEDULER_PERSIST = True
		【注】分布式爬取的时候，指令不是scrapy crawl xx
		scrapy runspider xxx.py
		在我的windows中往队列中添加起始url（此url为要爬取的网站的起始地址，很重要）
			lpush nnspider:start_urls "http://www.xxxxx.com/movie/
```

