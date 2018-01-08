title: 用Automator实现开机自动连接VPN
date: 2014-12-14 17:33:52
tags: AppleScript
---
自从Dropbox被墙之后，同步就成了一件很肉的事，而我总是忘记开VPN把文件同步到最新。为了搞一个工作流必须保证Dropbox一打开就自动同步，于是利用Mac自带的Automator中执行AppleScript来完成一个开机自动连接动作。

### STEP 1 
打开Automator，新建`应用程序`

![Automator](http://7qn9uj.com1.z0.glb.clouddn.com/media/automator-1.png)

### STEP 2 
在`实用工具`中选择`运行AppleScript`

### STEP 3
在脚本编辑器中填入

```
tell application "System Events"
    tell current location of network preferences
        set VPN to "MyVPN"
        set VPNactive to connected of current configuration of service VPN
        if VPNactive then
            disconnect service VPN
        else
            connect service VPN
        end if
    end tell
end tell
```
其中`MyVPN`为你的VPN服务名称

### STEP 4
取个名字，例如`Ladder`保存到应用程序文件夹

### STEP 5
给这个App弄一个炫酷的图标。
画一个icon或者找一个icon图片，用预览打开全选-复制，再右键点击App，打开显示简介，选中左上角的图标，粘贴。

![new icon](http://7qn9uj.com1.z0.glb.clouddn.com/media/automator-2.png)

### STEP 6
拖动图标到Dock上，设置登录时打开。这样开机之后VPN就可以自动连接了，也可以在Dock上快速操作连接/断开VPN。

![dock status](http://7qn9uj.com1.z0.glb.clouddn.com/media/automator-3.png)
