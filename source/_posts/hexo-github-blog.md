---
title: Hexo+GitHub博客搭建，多终端同步方案
date: 2017-11-01 11:33:18
tags: [hexo, Github]
---

之前搭建过一次，但是没有备份hexo设置，小白看了一圈，还是要重来，首要问题就是解决hexo文件同步，通过GitHub仓库建立两个分支，master是发布的博客文件，hexo分支放hexo文件。记录一下过程，所用系统都是windows的。
<!-- more -->

## 1、基础环境配置

### 1.1 安装node.js

在[node.js官网](https://nodejs.org/en/)下载并根据提示安装。

### 1.2 安装git

在[git官网](https://git-scm.com/)下载并根据提示安装，记得第一次安装时，有两个安装包需要安装，一个是git-lfs-windows，还有一个是git客户端。

### 1.3 配置ssh-key

- 注册GitHub账号

- 设置git的user name和email

  ```
  git config --global user.name "YOUR NAME"
  git config --global user.email "YOUR EMAIL ADDRESS"
  ```

- 生成密钥

  ```
  ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
  ```

- 将密钥添加到SSH-agent，依次输入以下两个命令：

  ```
  eval "$(ssh-agent -s)"
  ssh-add ~/.ssh/id_rsa
  ```

- 将密钥添加到GitHub账户

  - 拷贝ssh key：

    ```
    clip < ~/.ssh/id_rsa.pub
    ```

  - 添加到GitHub账号：点击GitHub头像 - Settings - SSH and GPG keys - Add SHH key，在title输入密钥名称，如`your_name - PC`，然后在Key里粘贴刚复制的SSH Key，点击Add SSH Key。

- 测试SSH连接

  ```
  ssh -T git@github.com
  ```



## 2、github配置

- 打开GitHub创建仓库（勾选README.md选项），命名为"yourname.github.io"，如resa.github.io
- 在项目页面，点击`1commit`下方的`branch: master`，添加`hexo`分支
- 在GitHub上将hexo设为默认分支：进入博客项目仓库 - Setting - Branchs - Default branch下拉选择hexo - Update -确定

## 3、安装hexo

建立your-user-name.github.io文件夹，打开文件夹，右键选择git bash here

- 执行hexo安装命令：

  ```
  npm install hexo-cli -g
  ```

- 初始化hexo：

  ```
  hexo init
  ```

- 安装hexo相关插件：

  ```
  npm install
  ```

- 安装deployer git：

  ```
  npm install hexo-deployer-git --save
  ```

- 生成网站：

  ```
  hexo g
  ```

- 启动本地服务器，默认可以通过`http://localhost:4000`查看博客demo

  ```
  hexo s
  ```

## 4、关联hexo与GitHub

### 4.1 修改hexo全局配置文件

用记事本或sublime等编辑器打开库文件夹中的_config.yml，修改Deployment（替换yourname，注意冒号后面要空一格）：

```
deploy:
    type: git
    repo: git@github.com:yourname/yourname.github.io.git
    branch: master
```

生成推送到github的master分支：

```
hexo g -d
```

打开自己的blog：`https://yourname.github.io`

### 4.2 hexo源码备份 

进入库文件夹，执行下列命令：

```
git init  //初始化本地仓库
git add --all 
git commit -m "Blog Source Hexo"
git branch hexo  //新建hexo分支
git checkout hexo  //切换到hexo分支上
git remote add origin git@github.com:yourname/yourname.github.io.git  //将本地与Github项目对接
git push origin hexo -f //将本地仓库的源文件分支hexo强制推送到远程仓库hexo分支
```

此时刷新GitHub博客项目就可以看到推送的hexo文件。

## 5、其他终端配置

此时在另一终端更新博客，只需要将Github的hexo分支clone下来，进行初次的相关配置：

```
git clone -b hexo git@github.com:yourname/yourname.github.io.git  //将Github中hexo分支clone到本地
cd  yourname.github.io  //切换到刚刚clone的文件夹内
npm install    //注意，这里一定要切换到刚刚clone的文件夹内执行，安装必要的所需组件，不用再init
```

如果是全新电脑，需要操作“1、基础环境配置”中的步骤，再进行上述命令操作。

## 6、不同终端博客更新

在不同的终端已经做完配置，就可以愉快的分享自己更新的博客，进入自己相应的文件夹：

```
git pull origin hexo  //先pull完成本地与远端的融合（此时当前分支应为hexo）
hexo new post "new blog name"   //新建一个.md文件，并编辑完成自己的博客内容
git add source  //经测试每次只要更新sorcerer中的文件到Github中即可，因为只是新建了一篇新博客
git commit -m "XX"
git push origin hexo  //更新分支
hexo g -d  //push更新完分支之后将自己写的博客对接到自己搭的博客网站上，同时同步了Github中的master
```

***

## 7、其他设置

### 7.1 hexo配置修改

打开_config.yml设置网站名称、描述、语言等：

```
title: yourname的博客
subtitle:
description: 网站描述
author: 作者名
language: zh-Hans
timezone: Asia/Shanghai
```

### 7.2 主题修改

- 示例：下载next主题

  ```
  git clone https://github.com/iissnan/hexo-theme-next themes/next
  ```

- 修改hexo配置文件_config.yml中的theme为next

  ```
  theme: next
  ```

- 修改主题配置文件，位置`themes/next/_config.yml`，具体可参考[next主题配置](http://theme-next.iissnan.com/theme-settings.html)

- PS. 第三方主题要把主题文件夹下面把.git文件夹删除掉，再推送

## 8、参考资料

- [使用Hexo & Github,搭建属于自己的博客](http://www.cnblogs.com/ld1024/p/5913169.html)
- [hexo你的博客](http://ibruce.info/2013/11/22/hexo-your-blog/)
- [Jekyll迁移到Hexo搭建个人博客](https://www.ezlippi.com/blog/2016/02/jekyll-to-hexo.html)
- [记录第一次搭建hexo](http://www.jianshu.com/p/017e01718d41)
- [手把手教你用Hexo+Github 搭建属于自己的博客](http://blog.csdn.net/gdutxiaoxu/article/details/53576018)
- [Hexo搭建Github-Pages博客填坑教程](http://www.jianshu.com/p/35e197cb1273)
- [搭建hexo博客并简单的实现多终端同步](https://righere.github.io/2016/10/10/install-hexo/)
- [如何解决github+Hexo的博客多终端同步问题](http://blog.csdn.net/Monkey_LZL/article/details/60870891)
- [多机更新 Hexo 博客](http://lowrank.science/Hexo-Migration/)
- [Hexo的版本控制与持续集成](https://formulahendry.github.io/2016/12/04/hexo-ci/) `待实践`

***
2018-11-1更新：
## 9、hexo更新
```
npm i hexo-cli -g
```

参考：
- [Hexo官网](https://hexo.io/)
- [Hexo文档](https://hexo.io/zh-cn/docs/)
- [Hexo升级之坑](http://zerosoul.github.io/2016/06/15/upgrade-hexo-to-3-2/)

## 10、next主题更新
之前是5.1.3版本的，直接升级发现木有变化，后来发现有6.0以上版本了，由于上次没有做多少配置，我直接删掉了原文件夹，然后重新安装next了：
```
$ cd your-hexo-site
$ git clone https://github.com/iissnan/hexo-theme-next themes/next
```

参考：
- [Next github](https://github.com/theme-next/hexo-theme-next)
- [Next 主题配置](https://theme-next.iissnan.com/theme-settings.html#use-bg-animation)
- [让你的Hexo博客华丽升级](https://juejin.im/entry/59e862ee6fb9a04517044f72)
- [Hexo Next主题5.X升级至6.X](https://my.oschina.net/m1c3/blog/1622488)
- [从 NexT v5.1.x 更新](https://github.com/theme-next/hexo-theme-next/blob/master/docs/zh-CN/UPDATE-FROM-5.1.X.md)
