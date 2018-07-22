---
title: Sublime sftp插件的使用
date: 2018-07-10 23:51:00
tags:
	- sftp
	- sublime
---


## 前言
sublime的sftp插件是我平时开发时使用率最高的几个插件之一，安装成功并且配置完成后，你可以直接在本地修改完代码，然后control+s保存，神奇的事情发生了，你的代码立刻同步到了你自己的测试服务器上。省下了你每次修改都要提交代码到测试服务器，然后等待自动化部署的时间，那得浪费我多少青春年华啊😂，直接在服务器上调试，开发效率大大提高了，废话不多说了下面我来介绍一下如何安装、配置、使用它吧。

### 安装

1.快捷键win使用(control+shift+p) Mac使用(command+shift+p) 打开插件控制面板
<!--more-->
<img src="http://pbnsa68r0.bkt.clouddn.com/sftp1.png" alt="">

2.在输入框中输入PCI打开Install Package，在输入框中输入sftp 你就会看到sftp插件，因为我安装过了所以没有显示，点击安装。

<img src="http://pbnsa68r0.bkt.clouddn.com/sftp2.png" alt="">

### 配置

1.选择你需要同步的文件夹，右击，如果你之前没有在这个文件夹下配置过sftp的话你会看到这个按钮，点击Map to Remote...,就会在你文件夹中生成sftp-config.json的配置文件。

<img src="http://pbnsa68r0.bkt.clouddn.com/sftp3.png" alt="">

2.下面我们就来配置sftp,看这个截图吧，文件中需要你配置的大概也就五六处地方。看图

<img src="http://pbnsa68r0.bkt.clouddn.com/sftp4.png" alt="">

"upload_on_save"  这个设置为true 可以在你control+S的时候自动上传；
"host"            你服务器的IP xxx.xxx.xxx.xxx;
"user"            你的用户名 一般是root
"password"        登陆虚拟机的密码
"port"            sftp默认是22端口
"remote_path"     这个对应的是你测试服务器上文件的对应目录，比如我本地的文件名叫blog，远程代码对应的文件夹在/opt/www/blog，这里就填/opt/www/blog

3.基本上到这里就大功告成啦，但是需要注意的是你们测试服务器需要支持ssh以及sftp，没有的话可以谷歌自行安装下。

### 问题

最近从WIN转战了Mac，在我的Mac上尝试使用sublime的sftp的时候，总是提示连接超时and失败，之前WIN上可没有这个问题呀，但是sublime没有日志提示啊！只是简单的提示连接超时😭，也不知道问题出在哪里，有点方啊！只有知道问题，才能解决问题，不然像一只无头苍蝇，既然sublime没有提示具体错误，那么我就要找一个可以提示具体问题的工具，思来想去，就去下了一个支持sftp上传文件的工具，客户端肯定会有具体信息提示，下了比较常用的FileZilla，然后使用它连接我的测试机，终于发现了问题，log里面提示了：
错误：Received unexpected end-of-file from SFTP server。
终于找到了问题，辣么就可以使用谷歌，百度大法啦！最终找到了解决办法。😄
#### 解决办法
ssh登录你的测试机
1. cd /etc/ssh 找到sshd_config文件
2. vi sshd_config
3. 找到 Subsystem sftp /usr/lib/openssh/sftp-server 这行代码，把/usr/lib/openssh/sftp-server 替换为 internal-sftp
4. 重启sshd service sshd restart
5. 打开网易云音乐 听首曲子 放松下吧

<img src="http://pbnsa68r0.bkt.clouddn.com/qutu.png" alt="">
<font size=2 face="黑体" color="#999">这里有一只超级厚脸皮的猫鼬，这货为了看风景，竟然把一名女游客的脑袋当瞭望台。端坐在人家头上瞭望远处的风景。</font>
