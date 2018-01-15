title: Hexo折腾记
date: 2018-01-15 17:59:39
tags: Hexo
---

## 双击同步混乱

混乱状态的出现

新年增加了一台MBP作为工作电脑，而家里的老MBA处于封印状态长达半年。

新老电脑一度使用Dropbox共享本地博客文件夹，似乎采用Dropbox和Github同时做版本管理会有诡异问题。

老MBA的node开发环境、hexo版本一律老化。

问题解决

1. 从旧电脑上备份博客个人数据

包括站点配置文件`_config.yml`，主题文件夹`theme/`，文章文件夹`source/`，文章模板`scaffolds/`，依赖包`package.json`，忽略提交的配置项`.gitignore`

2. 移除Dropbox里的博客，rm -rf hexoblog
3. 在本地新建一个

在Github的博客仓库建立2个分支，一个默认分支用于备份源文件，一个分支用于渲染静态文件。



## 远程仓库静态文件莫名其妙“回滚”

## 远程仓库主题文件夹同步失败

## tag冒号后面缺少空格导致渲染失败

## hexo-renderer-marked插件没删干净导致渲染失败



