---
title: hexo + github 搭建个人博客
date: 2017-11-29 10:40:51
categories: 其他
tags: [博客, hexo, github]
thumbnail: http://pic1.16pic.com/00/52/43/16pic_5243097_b.jpg
---
## GitHub
1. 创建GitHub账号，安装node环境，安装Git
2. 登录到GitHub，点击GitHub中的New repository创建新仓库，仓库名应该为：用户名.github.io 这个用户名使用你的GitHub帐号名称代替
3. 配置SSH key
检查是否存在密钥
```
$ cd ~/. ssh //检查本机已存在的ssh密钥
```
如果没有则创建密钥
```
$ ssh-keygen -t rsa -C "邮件地址"
```
最终会生成一个文件在用户目录下，打开用户目录，找到.ssh\id_rsa.pub文件，记事本打开并复制里面的内容，打开你的github主页，进入个人设置 -> SSH and GPG keys -> New SSH key，将刚复制的内容粘贴到key里。

  测试是否配置成功：
```
$ ssh -T git@github.com
```
如果提示
Are you sure you want to continue connecting (yes/no)?，
输入yes，然后如果看到这个信息：

 You've successfully authenticated, but GitHub does not provide shell access.
说明SSH已配置成功！

4. 此时你还需要配置：
```
$ git config --global user.name "github用户名"
$ git config --global user.email  "github注册邮箱"
```
## hexo
1. 安装
```
$ npm install -g hexo // 全局安装hexo
$ npm install -g hexo-cli // 全局安装hexo-cli
```
2. 初始化hexo
```
$ hexo init 文件名 // 创建一个hexo框架
$ cd 文件名
$ npm install // 安装依赖包
$ hexo generate // 生成静态文件（结果文件）【或者：hexo g】
$ hexo server // 启动本地服务，可以通过http://localhost:4000/ 访问 【或者 hexo s】
```
第一次初始化的时候hexo已经帮我们写了一篇名为 Hello World 的文章
3. 修改主题

  可以到官网上[hexo](https://hexo.io/themes/) 寻找自己喜欢的主题，或者自己编写主题。
  找到自己喜欢的主题的GitHub，并且在hexo文件目录中下载
  ```
  $ hexo clean //如果出现问题，先清理一下public的内容
  $ git clone github地址
  ```
  修改Hexo目录下的_config.yml配置文件中的theme属性为主题名字
  4. 配置hexo

    配置全局的_config.yml中deploy的部分，有两种写法：
    - 安装插件
    ```
    $ npm install hexo-deployer-git --save
    ```
    ```
    deploy:
      type: github
      repository: https://github.com/用户名/用户名.github.io.git
      branch: master
    ```
    - 不安装插件
    ```
    deploy:
      type: github
      repository: git@github.com:用户名/用户名.github.io.git
      branch: master
    ```
  5. 上传到GitHub
  在hexo目录下
  ```
  $ hexo d // 将本次有改动的代码全部提交，没有改动的不会
  ```
## hexo常见命令
```
$ hexo generate  // 简写：hexo g，生成静态文件，会在当前目录下生成一个public文件夹
$ hexo server       // 简写：hexo s，启动本地服务，用于博客的预览
$ hexo deploy       // 简写：hexo d，部署到远程（如GitHub，可以在_config.yml中配置）
$ hexo new post-name // 简写：hexo n post-name， 新建文章
$ hexo new page page-name   //简写：hexo n page page-name，新建页面
```
缩写
```
$ hexo n == hexo new
$ hexo g == hexo generate
$ hexo s == hexo server
$ hexo d == hexo deploy
```
组合命令
```
$ hexo d -g                 // 生成和部署
$ hexo s -g                 // 生成和预览
```
草稿命令
```
$ hexo new draft <title>        // 新建草稿，存放在source/_drafts
$ hexo publish post <title>     // 发布草稿为文章，文章转移到source/_posts
$ hexo s -g --drafts            // 显示草稿
```
## 新建博客
在hexo根目录下：
```
$ hexo new '博客名' // 生成 博客名.md
$ hexo new page "博客名" // 生产 博客名\index.html
```
我是前端工程师，所以自己是用atom编辑博客的，推荐使用哦~
