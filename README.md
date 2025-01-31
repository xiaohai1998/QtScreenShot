# Qt全屏截图器－By XFuture

![](.\Images\封面.png)

### 用途

快速捕捉全屏截图，分类存放，方便查找



### 使用方法

#### 截图页

![](.\\Images\\sc.png)

按下大箭头按钮即可捕捉全屏截图。全局快捷键为“Alt+S”

选择不同项目可以保存截图到不同的文件夹

选择项目菜单栏右侧的按钮点击后可以查看当前项目文件夹的大小

#### 截图设置页

![](.\\Images\\setting.png)

过渡补偿：窗口隐藏到触发截图有一段过渡动画，如果窗口没有完全消失，则生成的截图会有窗口的影子

*从点下”截图“按钮到触发截图的总时长为 ”延迟时间“ + ”过渡补偿“

文件格式：保存的截图的文件格式

保持置顶：是否保持窗口置顶

截图后提醒:截图完成后是否提醒

截图提醒方式：播放音频：截图完成后播放内置音频

​			   弹出消息：截图完成后弹出通知，点击可以打开刚刚的截图



#### 项目管理页

![](.\\Images\\manage.png)

管理项目

添加项目：在输入框里填写项目名称，点击添加项目即可添加

工作目录：程序保存项目文件夹的默认路径

迁移文件：选择源目录和目标目录，完成后自动从源目录迁移文件到目标目录

#### 菜单栏

![](.\\Images\\menu.png)

截图：字面意思

打开文件夹：打开存有项目文件夹的文件夹，该文件夹的实际位置在安装目录的“Picture”文件夹下

打开项目文件夹：打开当前选择的项目的文件夹，可以管理截图

刚刚的截图：打开最新的截图

退出：关闭程序

#### 添加开机自启动

一、在安装目录下有"添加开机自启动.bat"和"删除开机自启动.bat",选择对应的文件双击即可

二、当bat文件添加失败时，可以选择手动添加

​	有两种方式可供选择

​		1）手动操作：[Windows设置程序开机自启动](https://blog.csdn.net/weixin_45447477/article/details/122638366)

​		2）使用“RegAutoRun.exe"。这个程序在安装目录中，这是一个命令行工具使用时应打开此软件安装目录，按住Shift同时右键空白处，选择”在此处打开PowerShell窗口 (s)"，之后在Power Shell中输入命令启动，使用程序添加自启动的调用命令是

```
.\RegAutoRun.exe -add "Key Name" "Path of EXE file" "parameters"
```

​	删除自启动的命令是

```
.\RegAutoRun.exe -del "Key Name"
```

​	对于本程序，	因为软件自启动会更改工作目录，导致不能正常读取config.json文件

​	解决方案是在安装目录里新建“background_run.bat"文件，并填写以下内容

```
@echo off
cd /d %~dp0
start "" ".\ScreenShot.exe" "-background"
```

​	添加自启动时，调用命令应该是

```
.\RegAutoRun.exe -add "ScreenShotBGRun" "background_run.bat"
```

​	删除自启动的命令是

```
.\RegAutoRun.exe -del "ScreenShotBGRun"
```



### 提醒

不明白的话不要随意更改“config.json”文件里的内容，这可能导致文件编码错误，进而导致程序界面显示不正常。

如果出现这种情况，应打开程序安装目录，删除“config.json”，再次启动程序，重新添加以前的项目，再关闭即可生成新的文件。



### 参考

[ddqd/qxtglobalshortcut5: qxtglobalshortcut library qt5 compatibility (github.com)](https://github.com/ddqd/qxtglobalshortcut5)

### 更新日志

#### 20210731

-第一个可用的版本

#### 20220205

-更改了截图界面样式，增加了添加工作目录，迁移工作目录等功能

#### 20220812

-支持更改提醒方式，关闭时可隐藏至托盘，可以关闭截图提醒，提醒方式增加到两种（提示音和消息通													      知），修复了4.0版本自启动不能读取配置文件的bug