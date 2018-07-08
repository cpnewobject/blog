---
title: FIS-PLUS 前端自动化构建工具（一）安装
date: 2018-07-08 20:11:20
tags: 前端构建工具
---


## 前言

现在的前端开发已经不仅仅只是静态页面的开发，各种新的前端技术日新月异，前端代码逻辑和交互越来越复杂，模块化开发，各种框架，增加了最后发布的难度，这些都让前端项目结构难以管理。前端自动化构建在整个开发中越来越重要。

目前市面是主流的前端构建工具主要有 Webpack、Gulp、Grunt等等，FIS可能听过它的小伙伴比较少，特别对于初入行业一两年的来说，FIS是百度内部使用的前端构建工具，Fis-Plus是扩展自FIS的前端集成解决方案。其提供 后端框架、前端框架、自动化工具、辅助开发工具等开发套件，在那个前端构建工具还没有普及的年代，FIS在业界算是比较好的。由于公司内部一些项目比较老旧，这些老项目都是使用FIS构建的，初来公司的我面对FIS也是一脸懵逼，但是万变不离其宗，<!--more-->前端构建工具无非就是提供一些自动化处理，代码检查、预编译、合并、压缩；生成雪碧图、sourceMap、版本管理；运行单元测试、监控等，当然有的工具还提供模块化、组件化的开发流程功能，下面我们就来初步认识一下FIS-PLUS。

## 安装

FIS-PLUS 是基于FIS的，应用于后端是PHP，模板是Smarty的场景。

一、nodejs
这个不用多说了，现在还有不用node的前端嘛？？

二、npm
npm 是 nodejs 的包管理工具。安装nodejs后，npm就自动一起安装了。
这里多说一点，由于npm经常被墙，安装fis的时候会出现速度过慢，或者安装不上的问题。
这里推荐使用淘宝镜像安装，使用：
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
安装成功后就可以使用cnpm代替npm使用。

三、安装fis-plus
nodejs 安装好后，命令行执行
npm install -g fis-plus
安装好 fis-plus 之后，执行 fisp -v 能够看到版本号说明安装成功了 目前版本应该是v0.8.18

四、安装java环境
	[安装Java](https://www.java.com/zh_CN/)
	安装成功后执行 java -version 能够看到版本号说明已经安装成功

五、安装 php-cgi
	这里分为
*	Mac安装
	推荐使用直接下载XAMPP的方式进行安装
	[安装XAMPP](https://www.apachefriends.org/xampp-files/7.2.6/xampp-osx-7.2.6-0-installer.dmg)安装成功后需要配置环境变量，在命令行中；
	使用bash:
	$ echo 'export PATH=/Applications/XAMPP/bin:$PATH' >> ~/.bashrc
	$ source ~/.bashrc
	使用 zsh:
	$ echo 'export PATH=/Applications/XAMPP/bin:$PATH' >> ~/.zshrc
	$ source ~/.zshrc
	这两个都要配置一下
*	WINDOWS安装
	[安装XAMPP](https://www.apachefriends.org/xampp-files/5.6.36/xampp-win32-5.6.36-0-VC11-installer.exe)
	同样需要配置环境变量
	windows环境变量配置，将xampp/php路径加入环境变量中。

上面两个操作完，在命令行中输入php-cgi -v ，就看到php-cgi版本号。php-cgi就装好啦！

### 初始化项目
为了前后端开发分离，来并行开发，fis-plus 提供了一套本地环境模拟的工具，安装并初始化它后就能方便的模拟线上环境了。

以下示例都是在命令行下操作的，如果你是 windows 用户，请打命令的时候忽略命令前的 $，而且请打开cmd 来执行这些操作
$ fisp server init

### 下载 Demo
FIS 的所有示例及其组件都用包管理工具 lights 进行管理，使用 lights 安装 demo。
$ lights install pc-demo
其实 fisp 已经集成了 lights 的客户端。
和上面等值的用法；
$ fisp init pc-demo
fisp <= 0.7.5 
$ fisp install pc-demo
如果下载失败，可直接从 GitHub [下载](https://github.com/fex-team/fis-plus-pc-demo)

#### 发布
$ cd pc-demo
$ fisp release -r common
$ fisp release -r home
#### 预览
$ fisp server start #启动服务器
启动服务的时候，启动成功后会自动打开浏览器，访问首页，这时候你应该打开demo首页

## 结尾
今天主要介绍了Fis-Plus的安装以及项目的初始化，下一节我们就来更加深入的了解一下Fis-Plus的使用方法～～
