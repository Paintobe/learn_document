#### 使用事务

- 在保存订单数据时，涉及到多张表（商品表、订单表、订单详情表）据的修改应该是一个整体事务，即要么一起成功，要么一起失败。

- mysql中事务的使用

  ```python
  begin  # 开启事务
  rollback # 回滚事务
  commit  # 提交事务
  ```

- Django中事务的使用

  - with语句用法

    ```python
    from django.db import transaction
    
    def viewfunc(request):
      # 这部分代码不在事务中，会被Django自动提交
      ......
    
      with transaction.atomic():
          # 创建保存点
          save_id = transaction.savepoint()
          # 这部分代码会在事务中执行
          ......
          # 回滚到保存点
          transaction.savepoint_rollback(save_id)
          ......
          # 提交从保存点到当前状态的所有数据库事务操作
          transaction.savepoint_commit(save_id)
    ```

#### 使用乐观锁并发下单

- 在多个用户同时发起对同一个商品的下单请求时，先查询商品库存，再修改商品库存，会出现资源竞争问题，导致库存的最终结果出现异常。

- 解决办法：

  - 悲观锁：

    - 当查询某条记录时，即让数据库为该记录加锁，锁住记录后别人无法操作，使用类似如下语法

      ```python
      # 满足的条件
      # 1、必须在事务中使用
      # 2、select 后面加 for update
      select stock from sp_goods where id=1 for update;
      
      Goods.objects.select_for_update().get(id=1)
      ```

    - 悲观锁类似于我们在多线程资源竞争时添加的互斥锁，容易出现死锁现象，采用不多。

    - 比如用户A给表A加了锁，然后查询表B。用户B给表B加了锁，然后查询表A。两个人同时等待对方操作完后，解除锁。这样就产生了死锁

- 乐观锁：

  - 乐观锁并不是真实存在的锁，而是在更新的时候判断此时的库存是否是之前查询出的库存，如果相同，表示没人修改，可以更新库存，否则表示别人抢过资源，不再执行库存更新。类似如下操作

    ```python
    update sp_goods set stock=10 where id=1 and stock=20;
    
    Goods.objects.filter(id=1, stock=20).update(stock=10)
    ```

  - 操作条件：

    - 库存大于购买量，
    - 更新库存和销量时原始库存没变。

#### MySQL事务隔离级别

- 事务隔离级别指的是在处理同一个数据的多个事务中，一个事务修改数据后，其他事务何时能看到修改后的结果。

- MySQL数据库事务隔离级别主要有四种：

  - `Serializable`：串行化，一个事务一个事务的执行。
  - `Repeatable read`：可重复读，无论其他事务是否修改并提交了数据，在这个事务中看到的数据值始终不受其他事务影响。
  - `Read committed`：读取已提交，其他事务提交了对数据的修改后，本事务就能读取到修改后的数据值。
  - `Read uncommitted`：读取未提交，其他事务只要修改了数据，即使未提交，本事务也能看到修改后的数据值。
  - MySQL数据库默认使用可重复读（ Repeatable read）。

- linux修改方式：

  ![image-20190901182631928](/Users/apple/qianfeng/授课/sz1903/day06/资料/day06.assets/image-20190901182631928.png)

- mac修改方式

  ```python
  serializable 串行化
  repeatable read 可重复读
  read committed 读取已提交
  read uncommitted 读取未提交
  
  # 修改全局事务隔离级别
  set global transaction isolation level read committed;
  
  # 查看隔离级别
  select @@global.transaction_isolation;
  ```

