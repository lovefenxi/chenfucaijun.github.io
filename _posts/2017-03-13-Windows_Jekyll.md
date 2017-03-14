---
layout: post
title: "Windows下安装和使用Jekyll"
date:   2017-03-11 09:59:21 +0800
---

# [Windows下安装和使用Jeykll](http://jekyll-windows.juthilo.com/)

## 1.安装Ruby
> Jekyll3.0+要求Ruby2.0+

* 我选择下载[ruby2.3.3(x64)](https://dl.bintray.com/oneclick/rubyinstaller/rubyinstaller-2.3.3-x64.exe) 
* 其他Ruby版本[下载](http://rubyinstaller.org/downloads/)

* 安装过程中，记得勾选“Add Ruby executables to your PATH”
![勾选](http://i1.piimg.com/1949/ad54bd218964887b.png)



## 2.安装Ruby DevKit
* 我选择下载[DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe](https://dl.bintray.com/oneclick/rubyinstaller/DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe)
* 其他版本[下载](http://rubyinstaller.org/downloads/)
![Ruby DevKit](http://i1.piimg.com/576036/5871abc0232feb09.png)
* 安装时选择路径，记住该路径，比如我的是`C:\RubyDevKit`
![RubyDev安装路径](http://p1.bpimg.com/576036/3d60ac87ed9f878b.png)

## 3.安装完毕后，初始化DevKit，在Windows的cmd中输入以下指令,`C:\RubyDevKit`是刚安装的Ruby DevKit的目录
```
cd C:\RubyDevKit
ruby dk.rb init
ruby dk.rb install
```
安装过程如下图：
![Markdown](http://p1.bpimg.com/576036/44cde9b39c16a815.png)

## 4.安装Jekyll
在Windows的cmd中输入
```
gem install jekyll
```
安装完毕如下图：
![Markdown](http://p1.bqimg.com/576036/dcb5cce2ed73d5a5.png)

检查Jekyll 是否安装成功：
![Markdown](http://p1.bqimg.com/576036/f34a53d7c4985be9.png)

## 5.安装bundler,用于安装Jekyll工程的插件
* 命令行中执行`gem install bundler`

## 6.实例教学
> 下面来看一个Jekyll工程本地使用流程：

* 在c盘中新建一个Jekyll工程，如下图结构
![Markdown](http://i1.piimg.com/576036/6472e4d3d356ef65.png)
* Gemfile内容如下：
```
source 'https://rubygems.org'
gem 'github-pages', :group => :jekyll_plugins
```

* _config.yml内容如下:

```
title: 陈府才俊
email: chenlei163mail@163.com
baseurl:  
url:  

#分页要安装的插件
gems:
  - jekyll-paginate


#分页数
paginate: 2
paginate_path: '/blog/:num'

```

* 在添加完Gemfile后，要在当前工程路径下的CMD命令行中执行
`bundler install`
这步很重要，否则后面的步骤会报错！


# 6.CMD中进入到工程路径下执行jekyll命令
![Markdown](http://p1.bqimg.com/576036/1de4bb85689e7157.png)

```
jekyll build
jekyll serve
```

# 7.在浏览器中访问`http://127.0.0.1:4000/`
访问成功说明本地Jekyll工程运行成功
![Markdown](http://p1.bqimg.com/576036/d5217a4851d30547.png)


# 8.克隆到本地进行运行
* 比如你可以直接克隆我的[Jekyll项目](https://github.com/chenfucaijun/chenfucaijun.github.io),从cmd中进入到项目目录中，

```
bundler install
jekyll build
jekyll serve
```
