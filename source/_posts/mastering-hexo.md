title: Hexo驯服记
date: 2018-01-15 17:59:39
tags: [Hexo, blog]
---

> 折腾hexo的各种记录

## 多机同步混乱

工作和家用两台电脑电脑或者旧电脑换新电脑，如果想要同时维护博客，就很容易发生同步混乱。

### 思路：Git分支大法实现云端同步

首先搞清楚Hexo系统下和个人有关的数据文件，实际只包括：

- 根目录下的站点配置文件`_config.yml`
- 主题文件夹`theme/`
- 文章源文件夹`source/`
- 文章模板文件夹`scaffolds/`
- 依赖包数据文件`package.json`
- 忽略提交的配置文件`.gitignore` 

因此如果需要更换电脑或者新增作业电脑，只需要保存好以上几个文件夹，将它们备份到云端可以一劳永逸解决换电脑之忧。但Dropbox、百度云盘这种文件同步系统是不怎么可靠的，一旦同步失败你都不知道哪个版本才是最新的。

这里的最佳思路是在yourname.github.io仓库下使用2个分支，默认分支用于同步上面说的那些个人数据源文件，次分支来同步渲染静态页面（古典做法）。因为Github版本控制远远优于Dropbox。

具体步骤如下

### 第一步，旧电脑上配置流程

（假设GitHub已有名为yourname.github.io仓库，旧电脑博客目录名为hexoblog，且已升级为最新Hexo3.x）

1. 在GitHub的yourname.github.io上新建hexo分支，并设置为默认分支

   ![](http://7qn9uj.com1.z0.glb.clouddn.com/media/defaultbranch.png)

2. 编辑本地配置文件`_config.yml`，将默认分支设置为master

   ```yaml
   deploy:
     type: git
     repo: git@github.com:yourname/yourname.github.io.git
     branch: master
   ```

   

3. 删除根目录和主题目录下的.git文件夹（*主题目录这个有坑，解决办法见后）

4. 编辑根目录下的`.gitignore`  ，添加一行`public/`，目的是不用重复提交静态网页（已经在master分支了）

5. 将本地源文件更新到GitHub

```shell
git init
# 初始化git
git add. 
git commit -m "new branch"
git remote add origin git@github.com:yourname/yourname.github.io.git
# 关联远端hexo分支
git push -u origin master
# 如果报错，换git pull --rebase origin master
```

### 第二步，新电脑建站流程

1. 安装配置Git环境

2. 建议使用SSH而不是HTTP方式来访问服务器，因此需要更新本机SSH key到GitHub账号下，参考[官方指南](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)即可。

3. 安装Nodejs（或者当然最好用nvm来管理Nodejs）

4. 下载博客源文件

   ```shell
   git clone git@github.com:yourname/yourname.github.io.git 
   ```

   安装Hexo，但不要执行hexo init初始化，否则就重复建站了

   ```shell
   npm install -g hexo-cli
   npm install
   npm install hexo-deployer-git --save
   # 如果使用git submodule管理主题，加一步：
   # git submodule update --init --recursive
   ```

   至此新旧电脑数据完全一致

### 第三步，日常博客修改和发布

1. 在hexo目录下执行`git checkout hexo`，保证当前本地分支为默认分支hexo

2. 确认本地源文件更新为最新

   ```shell
   git pull
   # 如果使用git submodule管理主题，加一步：
   # git submodule update
   ```

3. 进行正常的新建或者修改博客，比如新建一篇博客 `hexo new post`，或者修改配置文件

4. 发布所有修改到GitHub hexo分支

```shell
git add . 
git commit -m "add a new post" 
git push origin hexo
# 这里不是push到master，别搞错了
```

5. 不用切换分支，将渲染好的静态文件发布到GitHub master分支，完成网站发布

```shell
hexo clean
#清除缓存
hexo generate
hexo deploy
# 或者hexo g -d
```

实际上还有一些省事的办法，只是为了加深对git命令的记忆，我还是选择了这个解决方案。

参考资料

> [知乎：使用hexo，如果换了电脑怎么更新博客修改](https://www.zhihu.com/question/21193762)
>
> [hexo多设备同步与版本控制实现](http://zealscott.com/posts/1708/)
>
> [Hexo-Github建博客教程](https://yaro97.github.io/2017/01/07/Hexo-Github%E5%BB%BA%E5%8D%9A%E5%AE%A2%E6%95%99%E7%A8%8B/)

## 第三方主题管理问题

Hexo第三方主题大多数发布在GitHub上，然而如果采用git clone下载到theme文件夹内，由于这些theme本身就是一个repo，自带的.git会和Hexo的母.git冲突，本地修改之后，无法push到GitHub远端。

如果你坚持使用git clone或者直接下载release包，那么可以简单粗暴删掉主题文件夹下的 .git 和.gitignore文件，坏处是如果原主题作者更新了你得自己再次手动下载重新配置主题文件。如果你不记得之前的配置改动，比如某个css里几个高度，可能就会导致主题乱掉。

另一种更优雅的办法是使用`git submodule`，把主题仓库当作博客仓库的一个子仓库，单独进行版本管理和同步。

1. Fork 一份作者的主题到自己的GitHub上，例如even这个主题

2. 为主题创建一个submodule

   ```shell
   git submodule add https://github.com/ahonn/hexo-theme-even themes/even
   ```

3. 创建完毕后，GitHub上的even会多一个尾巴

   ![](http://7qn9uj.com1.z0.glb.clouddn.com/media/submodule.png)

4. 至此submodule配置完毕，今后在不同电脑之前同步主题只需要

   ```shell
   git pull
   git submodule update
   # 如果是全新电脑安装完hexo之后 再执行一步：
   # git submodule update --init
   ```

   最后只剩一个问题，如果原作者更新了主题，就采取常规git fork合并冲突的方法。一般很少更新，就不详细描述了。

参考资料

> [使用 submodule 管理 Hexo 主题](http://www.swiftyper.com/2017/07/25/managing-hexo-theme-using-submodule)
>
> [Submodule 解决 Hexo 主题库更新](https://qbug.cf/2017/07/31/submodule-%E8%A7%A3%E5%86%B3-hexo-%E4%B8%BB%E9%A2%98%E5%BA%93%E6%9B%B4%E6%96%B0/)
>
> [Fork别人的主题代码 原作者更新后如何同步](https://blog.csdn.net/lw_chen/article/details/51239657)

## 愚蠢的markdown标点符号错误

这是一个很蠢的问题，Hexo生成的新mardown文件，会自动有一个tag行，但`tag: []`和后面的标签、方括号之间是应该要有空格，否则提交渲染的时候会提示渲染失败。

错误示范

单个标签tag:abc  

多个标签tag:[abc, def]

正确示范

单个标签tag: abc 

 多个标签tag: [abc, def]

类似蠢问题，[这位也遇到了](http://www.swiftyper.com/2017/07/30/hexo-tip-do-not-using-square-brace-in-title/)，就是不要在标题行用方括号。

## hexo-renderer-marked插件没删干净

这算是一个hexo renderer的小bug，升级Hexo3.x以后，旧版hexo-renderer-marked需要手工卸载删除，否则会导致文章渲染失败。

```shell
npm uninstall hexo-renderer-marked --save
```

## GitHub Pages HTTPS的配置bug

GitHub Pages开始支持免费解析HTTPS，但按照官方指导会出现`Enforce HTTPS` 选项置灰无法勾选的情况。这应该是个bug。

![](http://7qn9uj.com1.z0.glb.clouddn.com/media/enforcehttps01.png)

问题解决

1. 首先到域名服务商那里删掉以前DNS的A记录，重新解析到新的IP地址

   ```ip
   185.199.108.153
   185.199.109.153
   185.199.110.153
   185.199.111.153
   ```

2. 尽管你的域名服务商表示已经解析完成，但GitHub可能要过2天左右才能完成解析，如果一直显示：

   > Enforce HTTPS — Not yet available for your site because the certificate has not finished being issued

3. 你就再等1天警告才会消失 ，但`Enforce HTTPS` 选项可能依然是灰的，这就是GitHub的bug了。这时候需要删掉已经填写好的域名，点一次`Save`，方框就可以勾选了

4. 重新添加一次域名，同时勾选上`Enforce HTTPS` 之后再点`Save`。成功

5. 之后https可以访问了但会提示证书无效，依然要过一段时间才能变绿

   ![](http://7qn9uj.com1.z0.glb.clouddn.com/media/enforcehttps02.png)


