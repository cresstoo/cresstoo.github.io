title: 通过AppleScript快速创建和发布Hexo文章
date: 2017-12-21 14:51:01
tags: hexo
---
因为给2018年定了一个要做**输出型人**的小目标，最近又开始对搁置了2年的博客不折腾不舒服斯基了。

<!-- more -->

先是由于换了电脑，重装nodejs和npm，Hexo从2.0升级到了3.0，按照[官方指引](https://github.com/hexojs/hexo/wiki/Migrating-from-2.x-to-3.0)完成了升级迁移。经过2年的变化，本人早就换了Bear作为主力笔记软件，还付费订阅了一年的服务。昨天折腾的时候发现Bear导出的Markdown文档meta信息乱掉了，分隔符会从`---` 变成 `- - - -`  从而导致发布显示错误。无奈之下只能放弃Bear作为Hexo文章编辑器，转向轻量级的专业Markdown编辑器Typora。

万事大吉，可以开始写东西啦。

### 回忆一下Hexo的使用命令

1. 打开终端，切换到Hexo的目录（有的人还会有切换env的步骤）

  `$ cd ~/Hexoblog`

2. 输入命令行，创建新文章

  `$ hexo new hello1984`

3. 用Typora打开hello1984.md，编辑保存

4. 输入命令行，发布文章（有时候还需要清理缓存）

  `$ hexo clean `

  `$ hexo d -g`

开启和执行终端命令实在有点繁琐啊喂，于是在想能不能也跟[以前一样通过Automator偷点懒](http://duran.im/2014/12/14/VPN-automator/)呢？于是做了点功课，参考这两个po主的代码（其实基本就拿来了）进行实现。其实尝试过程还是比较痛苦的，本意是想用iTerm而不是自带终端，谁知网上大多数iTerm的AppleScript脚本案例都在3.0版iTerm下报错了，建议还是用Mac系统自带的终端。

具体方法就是打开Automator，选择`运行AppleScript`，粘贴下面的代码就OK了。

### Hexo快速创建脚本

```app
tell application "Finder"
	activate
	display dialog "先想个好标题" default answer ""
	set title to text returned of result as text
end tell
tell application "Terminal"
	activate
	if (count of windows) is 0 then
		tell application "System Events"
			keystroke "n" using {command down}
		end tell
	else
		activate
	end if
	set win to window [0]
	set currentTab to selected tab of win
	-- 在当前 Tab 中执行改变目录的操作（需修改到自己的 Hexo 所在路径）
	do script "cd ~/Hexoblog" in currentTab
	do script "hexo new " & title in currentTab
	delay 1
	do script "open -a Typora source/_posts/" & title & ".md" in currentTab
	delay 3
	close windows
end tell
```

### Hexo一键发布脚本

```
tell application "Terminal"
	do script ""
	activate
	set win to window [0]
	set currentTab to selected tab of win
	-- 在当前 Tab 中执行改变目录的操作（需修改到自己的 Hexo 所在路径）
	do script "cd ~/Hexoblog" in currentTab
	do script "hexo clean " in currentTab
	delay 5
	do script "hexo d -g " in currentTab
end tell
```

最后用Automator导出为应用程序，顺便DIY俩图标，放在Dock上，愉快地开始码字了。

### 参考代码

> - [使用 AppleScript 制作自动脚本发布 Hexo]()
> - [AppleScript实现hexo新建/发布工作流](http://hunnble.github.io/2016/12/08/AppleScript%E5%AE%9E%E7%8E%B0hexo%E6%96%B0%E5%BB%BA-%E5%8F%91%E5%B8%83%E5%B7%A5%E4%BD%9C%E6%B5%81/)