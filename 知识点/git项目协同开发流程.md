#### git项目协同开发简易流程

- 项目管理者在码云或者github上面创建项目

  - master:  主干分支, 用来发布项目到线上，只有项目管理员可以操作
  - develop：测试分支，用来测试功能，项目组人员只能把代码推送到该分支

- 项目管理者把项目clone到本地

  ```python
  git clone http://xxx  或  git clone ssh://xxx(如果配置了密钥)
  ```


- 项目管理者在本地创建并切换到develop分支，把代码push到码云上面

  ```python
  git checkout -b develop
  git push origin develop
  ```


- 项目组的开发人员初始化代码需要clone项目到本地，以后在修改代码之前，必须先pull以下最新的代码，防止冲突

  ```python
  git clone http://xxx   或  git clone ssh://xxx(如果配置了密钥)
  ```

- 项目组开发人员创建并切换到develop分支，拉取码云上develop分支上的代码

  ```python
  git checkout -b develop
  git pull origin develop
  ```


- 项目组开发人员开发功能，完成后把代码push到码云的develop分支

  ```python
  git push origin develop
  ```


- 项目完成后，项目管理者从码云的develop分支拉取代码，并测试功能

  ```python
  git pull origin develop
  ```


- 项目管理者测试没问题，切换到本地的master分支，合并develop分支的代码。

  ```python
  git checkout master
  git merge develop
  ```


- 项目管理者把代码推送到码云的master分支

  ```python
  git push
  ```


- 项目管理者操作线上服务器，拉取码云的master分支的代码

  ```python
  git pull
  ```

