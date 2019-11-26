#### 支付宝支付

- 支付宝开放平台入口

  ```python
  https://open.alipay.com/platform/home.htm
  ```

- 登陆后创建沙箱环境

  ![image-20190901192404605](/Users/apple/qianfeng/授课/sz1903/day06/资料/day06.assets/image-20190901192404605.png)

- 沙箱环境

  - 支付宝提供给开发者的模拟支付的环境。跟真实环境是分开的。

  - 沙箱应用：https://openhome.alipay.com/platform/appDaily.htm?tab=info

    ![image-20190901192525607](/Users/apple/qianfeng/授课/sz1903/day06/资料/day06.assets/image-20190901192525607.png)

  - 沙箱账号：https://openhome.alipay.com/platform/appDaily.htm?tab=account

    ![image-20190901192605359](/Users/apple/qianfeng/授课/sz1903/day06/资料/day06.assets/image-20190901192605359.png)

- 支付宝开发文档

  - 文档主页：https://openhome.alipay.com/developmentDocument.htm
  - 电脑网站支付产品介绍：https://docs.open.alipay.com/270
  - 电脑网站支付快速接入：https://docs.open.alipay.com/270/105899/
  - API列表：https://docs.open.alipay.com/270/105900/
  - SDK文档：https://docs.open.alipay.com/270/106291/
  - Python支付宝SDK：https://github.com/fzlee/alipay/blob/master/README.zh-hans.md
    - SDK安装：pip install python-alipay-sdk --upgrade

- 电脑网站支付流程

  ![image-20190901193918155](/Users/apple/qianfeng/授课/sz1903/day06/资料/day06.assets/image-20190901193918155.png)



- 配置RSA2公私钥

  - 商城私钥加密数据，商城公钥解密数据。

  - 支付宝私钥加密数据，支付宝公钥解密数据。

    ![image-20190901194438310](/Users/apple/qianfeng/授课/sz1903/day06/资料/day06.assets/image-20190901194438310.png)

  - 生成商城公私钥

    ```python
    $ openssl
    $ OpenSSL> genrsa -out app_private_key.pem 2048  # 制作私钥RSA2
    $ OpenSSL> rsa -in app_private_key.pem -pubout -out app_public_key.pem # 导出公钥
    
    $ OpenSSL> exit
    ```

  - 配置商城公私钥

    - 配置商城私钥

      - 在根目录新建alipay文件夹用于存储公私钥。
      - 将制作的商城私钥`app_private_key.pem`拷贝到alipay文件夹中。

    - 配置商城公钥

      - 将`app_public_key.pem`文件中内容上传到支付宝。

        ![image-20190901194819062](/Users/apple/qianfeng/授课/sz1903/day06/资料/day06.assets/image-20190901194819062.png)

    - 配置支付宝公钥

      - 将支付宝公钥内容拷贝到`alipay_public_key.pem`文件中。

      ![image-20190901194926147](/Users/apple/qianfeng/授课/sz1903/day06/资料/day06.assets/image-20190901194926147.png)

      ```python
      -----BEGIN PUBLIC KEY-----
      支付宝公钥内容
      -----END PUBLIC KEY-----
      ```

    - 配置公私钥结束后

      ![image-20190901195049308](/Users/apple/qianfeng/授课/sz1903/day06/资料/day06.assets/image-20190901195049308.png)

    

  - 后端接口实现

    ```python
    def pay(request):
        alipay = AliPay(
            appid='2016092700609211',
            app_notify_url=None,  # 默认回调url
            app_private_key_path=os.path.join(settings.BASE_DIR, "alipay/app_private_key.pem"),
            alipay_public_key_path=os.path.join(settings.BASE_DIR, "alipay/alipay_public_key.pem"),
            sign_type="RSA2",
            debug=True
        )
    
        # 生成登录支付宝连接
        order_string = alipay.api_alipay_trade_page_pay(
            out_trade_no='订单号',
            total_amount='订单金额',
            subject='标题',
            return_url='同步回调地址',
        )
    
        alipay_url = 'https://openapi.alipaydev.com/gateway.do?' + order_string
        return redirect(alipay_url)
    ```

  - 同步回调地址验证

    - 注意：验证是否支付成功应该在异步回调接口验证，验证规则和同步的验证规则一样

      ```python
      def alipayback(request):
          query_dict = request.GET
          data = query_dict.dict()
      
          print(data)
          # 获取并从请求参数中剔除signature
          signature = data.pop('sign')
      
          # 创建支付宝支付对象
          alipay = AliPay(
              appid='2016092700609211',
              app_notify_url=None,  # 默认回调url
              app_private_key_path=os.path.join(settings.BASE_DIR, "alipay/app_private_key.pem"),
              alipay_public_key_path=os.path.join(settings.BASE_DIR, "alipay/alipay_public_key.pem"),
              sign_type="RSA2",
              debug=True
          )
          # 校验这个重定向是否是alipay重定向过来的
          success = alipay.verify(data, signature)
          if success:
              #	验证成功
              # 生成支付记录，改变订单状态
              print('yes')
              return render_json('yes')
          else:
            	# 验证失败
              print('no')
              return render_json('no')
      ```

      