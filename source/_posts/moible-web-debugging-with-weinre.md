title: 移动网页真机调试之Weinre
date: 2014-11-08 16:30:21
tags: debug
---
在进行移动网页开发的时候，利用Chrome自带的Emulation在PC上进行调试是非常方便的。而在Mac上利用Safari的开发功能，也可以实现在移动设备的Safari同步调试效果。但是Chrome无法替代真机效果，而Safari大法无法支持其他App的webview效果（除非你是该App的开发者），Android等其他设备的需求也无法满足。[Weinre](http://people.apache.org/~pmuellr/weinre/docs/latest/)是一个强大的网页调试工具，可以实现跨终端的远程调试，配合搭建本地服务器，更可以方便地直接在手机上调试本地代码。只需要简单的几步设定，产品人员也可以把真机调试掌握在手，拒绝webview的各种坑。以下为Mac下的简单教程。
<!--more-->

###	利用Node.js+Express快速搭建本地服务器环境

1.	下载并安装[node.js](http://nodejs.org)，不过建议使用nvm安装，不会弄乱你的Node版本。
2.	`npm install express` 安装Express。
3.	`express project` 新建网页项目。
4.	`cd project && npm install` 为项目搭建Web环境。
5.	在`project/public`文件夹下进行开发，或者将已有的源代码放入文件夹。
6.	`npm start` 启动Web服务器。
7.	访问`http://localhost:3000`，就可以看到本地网页了。

###	安装配置Weinre

1.	`sudo npm -g install weinre` 安装Weinre
2.	`weinre --boundHost -all-` 绑定本机当前IP地址
3.	`weinre --httpPort 8081` 指定Weinre服务器端口或者使用默认的8080
4.	访问 `http://本机IP地址:8081`，打开Weinre的主界面
5.	将Target Script的拷贝下来，嵌入到需要调试的网页中。例如，把`<script src="http://本机IP地址:8081/target/target-script-min.js#anonymous"></script>`放入index.html的底部。
6.	打开`http://本机IP地址:8081/client/#anonymous`，进入调试界面。此时因为没有在移动设备上还没有访问，所以Targets是none。
7.	打开你的手机，保证手机与电脑是同一IP域（同一个wifi路由器），用浏览器访问`http://本机IP地址:3000`，或者把这个url发到你需要测试的微信、手Q等App打开。
8.	刷新Weinre调试界面，Targets处应该就出现你的手机正在访问的信息。
9.	然后就可以进入Elements开始快乐地debugging啦，手机上会同步调试效果。

###	参考资源

[强烈推荐：无线调试攻略](http://thx.github.io/mobile/debugging-in-mobile/)
[五个你必须知道的javascript和web debug技术](http://js8.in/2013/11/20/%E4%BA%94%E4%B8%AA%E4%BD%A0%E5%BF%85%E9%A1%BB%E7%9F%A5%E9%81%93%E7%9A%84javascript%E5%92%8Cweb-debug%E6%8A%80%E6%9C%AF/)
[使用Weinre调试Mobile Web](http://www.iinterest.net/2012/02/08/debugging-mobile-web-applications-with-the-weinre/)
[使用 Weinre 调试移动网站及 PhoneGap 应用](http://www.cnblogs.com/lhb25/p/debug-mobile-site-and-app-with-weinre.html)
[nvm安装和使用](https://github.com/creationix/nvm)
