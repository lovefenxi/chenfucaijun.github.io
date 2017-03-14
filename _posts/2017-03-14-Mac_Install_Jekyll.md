---
layout: post
title: "Mac下安装和使用Jekyll"
date:   2017-03-11 09:59:21 +0800
---

# Mac下安装和使用Jekyll
* Mac自带了Ruby,gem,可直接执行下面的指令

```
sudo gem install jekyll
    
```

> jekyll安装完毕!

* 如何执行Jekyll程序?
    *  首先要新建一个Gemfile文件,用来指明要下载的Jekyll依赖,Gemfile一般内容如下:
   
    ```
    source 'https://rubygems.org'    
    ruby RUBY_VERSION
    
    # 分页依赖
    gem "jekyll-paginate"
    
    # 生成网站导航
    gem "jekyll-sitemap"
    ```
    *  然后安装这些依赖,在此之前还要安装一个bundler(ruby包管理器)
    
    ```
    sudo gem install bundler
    ```
    
    * 安装依赖
    ```
    bundler install
    ```
    * 执行jekyll命令
    ```
    jekyll build
    jekyll serve
    ```
* Mac中执行Jekyll可能出错,那么可以执行下面语句,作用等同于先build再serve
    ```
    bundle exec jekyll serve
    ```
    

