---
layout: post
title: "陈府才俊的博客:GithubPages的基本搭建"
date:   2017-03-11 09:59:21 +0800
---
# 基于Github Pages+Jeykll 搭建个人博客


# 前提技能及环境要求:
* 会基本的Github操作(克隆,提交等)
* 每人电脑中配置好Jekyll环境
    *  Linux安装Jekyll环境
    [在 Ubuntu 14.04 安装 Jekyll 3](https://hanbingyan.github.io/2016/04/04/jekyll/)

    *  Mac安装Jekyll环境
    [Install Jekyll on Mac](https://spinalhdl.github.io/SpinalDoc/mydoc_install_jekyll_on_mac/)

    *  Windows安装Jekyll环境
    [Windows下安装Jekyll环境](http://chenfucaijun.github.io/2017/03/11/chenfucaijun.html)
    

## 前言
* 搭建个人主页至少需要购买域名、服务器空间
* 搭建一个博客网站,涉及一系列的服务器配置,复杂的文章管理
* 解决以上问题,Github Pages是个不错的选择


## Github Pages是什么?


* [GitHub Pages](https://pages.github.com/)官网介绍
> 它是托管在Github上的静态网页,可以直接从Github仓库里的代码生成网页(展示项目主页)


* Github Pages的优点
    * 使用免费的username.github.io作为域名(也可绑定自己域名)
    * 无需自己搭建服务器,每个站300MB免费空间
    * 轻量级的博客系统,无麻烦的配置
    


* 快速建立Github Pages个人主页
    * [创建一个仓库](https://github.com/new),仓库名为*username*.github.io
    
    * 克隆该仓库,新建**index.html**,书写个人主页的内容,并提交
    ```
    # 克隆仓库
    git clone https://github.com/username/username.github.io
    
    # 书写内容至index.html
    cd username.github.io
    echo "Welcome!" > index.html
    
    # 提交代码
    git add --all
    git commit -m "first commit"
    git push origin master
    ```
    * 访问主页域名
    `http://username.github.io.`


* 你可以直接加入自己的css和js,
    * 比如:新建文件夹css,在css文件夹下新建mystyle.css
        ``` 
    body{
            margin: 0 auto;
            width: 70%;
    }
        ```
    * 在index.html中引入样式(相对路径)
 ``` 
     <!doctype html>
     <html lang="en">
     <head>
         <meta charset="UTF-8">
         <meta name="viewport"
               content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
         <meta http-equiv="X-UA-Compatible" content="ie=edge">
         <link rel="stylesheet" type="text/css" href="css/mystyle.css">
         <title>Document</title>
     </head>
     <body>
       Welcome! This my Github Pages Home!
     </body>
     </html>
 ```


* 那么Github Pages 背后的原理究竟是什么?
    * 仅仅是单纯的HTML+CSS+JS的渲染吗? 答案是:


# No
* 答案之一:它其实是通过**Jekyll**（发音/'dʒiːk əl/，"杰克尔"）这种软件进行转换网页源码生成静态文件,遵循的是Jekyll规范
(还有[Hexo](https://hexo.io/),[Octopress](http://octopress.org/)等等)
* Github Pages官网推荐使用Jekyll



## [Jekyll](http://jekyll.com.cn/)基本结构介绍



* Jekyll的基本使用
    * 命令行中Jekyll常用[指令](http://jekyll.com.cn/docs/usage/)

```
jekyll build
# => 当前文件夹中的内容将会生成到 ./site 文件夹中。

jekyll serve
# => 一个开发服务器将会运行在 http://localhost:4000/

```


* Jekyll的[目录结构](http://jekyll.com.cn/docs/structure/)
```
.
├── _config.yml   
|   
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   └── post.html
├── _posts
|   ├── 2017-03-09-chenfucaijun.md
|   └── 2017-03-10-zhangsanlisi.md
|   
├── _site
└── index.html
```


* 这些个目录结构的[作用](http://jekyll.com.cn/docs/structure/):
    * _config.yml:保存[配置](http://jekyll.com.cn/docs/configuration/)数据。
    * _includes:用来保存一些代码被其他文件重用。比如使用这个Liquid标签基本结构
  {% include head.html %} 来把文件 _includes/head.html 包含进来。
    * _layouts:layouts:是包裹在文章外部的模板。布局可以在 [YAML头](http://jekyll.com.cn/docs/frontmatter/)信息中根据不同文章进行选择。
    * _posts: 这里放的就是你的博客文章了。必须要符合: YEAR-MONTH-DAY-title.MAKEUP这样的格式,后缀名是md等标记语言
    * _site:一旦 Jekyll 完成转换，就会将生成的页面放在这里（默认）。最好将这个目录放进你的 .gitignore 文件中。
    * index.html: Jekyll启动时的入口文件,还可以通过YAML头指定其他入口


* [Liquid](https://help.shopify.com/themes/liquid/basics)的介绍
    * Tag标签:用于执行命令或者处理格式: {% 命令 %}
    ```
    {% if user.name == 'tom' %}
        Hey Elvis
    {% endif %}
    ```
    * Objects标签:用于输出内容: {% 一对尖括号内一对百分号 %}
        ```
        {{ site.title }} <!-- 输出: 网站的标题-->
        ```
    * [过滤器](http://jekyll.com.cn/docs/templates/),用于对输出内容做一些格式处理,用于Objects标签
        ```
        <!-- 网站标题会输出全大写 -->
        {{ site.title | upcase }}
        ```


* 在这两行的三虚线之间，你可以设置一些预定义的变量,或者甚至创建一个你自己定义的变量。
* 接下来的文件和任意模板中或者在包含这些页面或博客的模板中都可以通过使用 Liquid 标签来访问这些变量。
  
  ```
  ---
  <!-- 意指该文件使用的是layout中的default.html布局模板 -->
  layout: default
  title: Blogging Like a Hacker
  ---
  ```


* 看文档很枯燥,下面我们一起来动手,通过Jekyll写一个博客网站
    * 倘若你**安装了Jekyll环境**,那么你可以实时查看网页情况
    * **没有安装Jekyll**也没关系,只要语法正确,提交到github.io仓库中,也能实时查看网页情况



## 实例:使用[Jekyll](http://jekyll.com.cn/)搭建博客


* 使用Jekyll的模板,重用主页代码
    * 首先构造Jekyll的基本目录结构,
        * 之前已经创建了index.html和css/mystle.css,
    现在创建文件夹及其他文件如下
    ```
    .
    ├── _includes
    |   └── head.html
    ├── _layouts
    |   ├── default.html
    ├── _pages
    |   ├── about.md
    ├── _posts
    |   ├── 2017-03-09-chenfucaijun.md
    |   └── 2017-03-10-zhangsanlisi.md
    ├── css
    |   ├── mystyle.css
    |── _config.yml   
    |── Gemfile
    |── index.html
    ```


* 我们修改Gemfile和__config.yml内如下
    * Gemfile:指定安装好Github Pages运行Jekyll程序的所有依赖
    ```
    source 'https://rubygems.org'
    gem 'github-pages', :group => :jekyll_plugins
    ```
    * _config.yml:Jekyll的一些全局全局
    ```
    title: 陈府才俊
    baseurl:  # 你的网站的主页的子路径 比如:/blog
    url:  # 你的网站的域名
    
    ```


* `_includes/head.html`内容如下
 ```
 <head>
          <meta charset="UTF-8">
          <meta name="viewport"
                content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
          <meta http-equiv="X-UA-Compatible" content="ie=edge">
          <title>document</title> 
           <!--append过滤器:字符串后面加上内容 e.g.{{'bar'|append: 'foo'}}#=> 'barfoo'-->
  
          <link rel="stylesheet" href="{{ site.baseurl| append: "/css/mystyle.css"}}">
 </head>    
 
 ```   


* `_layouts/default.html`的内容如下:

```
<!doctype html>
<html lang="en">

<!--include 直接包含了_include/head.html的代码-->
{% include head.html%}  
<body>

<div class="page-content">
    <div class="wrapper">
        <!--content定义模板中可变内容,引用者进行添加内容-->
        {{ content }}
    </div>    
</div>
</body>
</html>
```


* index.html中内容如下

```
---
layout: default  
title: index
---
<!--layout指明引用哪个模板-->
<!--下面的内容会添加到{{content}}所在的位置-->
<h1>Welcome to my home page! I am </h1>
<p>This moment nap, you will have a dream. But this moment study, you will interpret a dream. 此刻打盹，你将做梦；而此刻学习，你将圆梦。  　　
</p>

```


* 本地运行Jekyll指令,进行预览 或者 直接提交至Github预览

```
    #Mac或者Linux
    bundle exec jekyll serve 

    #Windows进入到过程目录中
    jekyll build
    jekyll serve
    
    本地访问`http://127.0.0.1:4000
    上传Github Pages后访问http://username.github.io/

```


* 添加个人主页方法1:`_pages/about.md`文件内容如下
    * permalink:指定该页面永久链接, *有个坑!*
                  
```
---
layout: default
title: About
permalink: /about/                       
---
About Me
```

* 添加个人主页方法2:根目录下新建`/about/index.md`,内容中可以没有 `permalink: /about/` ,jekyll会自动寻找/about/中的index.html
```
├── about     
|   └── index.md 
```


* jekyll运行后,本地访问`http://127.0.0.1:4000/about/`
* 上传Github Pages后访问`http://username.github.io/about/`


* 注意:_pages中添加网页,必须要在`_config.yml`设置如下:
```
include:
  - _pages #转换时强制包含某些文件、文件夹
```


* 添加导航代码块:`_includes/header.html`
    * 
```
<header class="site-header header-nav">
    <nav class="site-nav">

        <div class="trigger">
            <!--site.baseurl相对路径-->
            <a href="{{site.baseurl | append: '/'}}">Index</a>
            <a href="{{site.baseurl | append: '/about/'}}">About</a>
            <a href="{{ site.baseurl | append: '/blog/'}}">Blog</a>
        </div>
    </nav>

    <!--头像-->
    <div class="wrapper">
        <div class="author">
            <a href="{{ site.baseurl | append: '/' }}">
                <amp-img class="avatar avatar i-amphtml-element i-amphtml-layout-responsive i-amphtml-layout-size-defined i-amphtml-layout" src="{{ site.baseurl | append:'/assets/photo.png'}}" width="90" height="90"
                         layout="responsive" alt="{{ site.title }}">
                    <i-amphtml-sizer style="display: block; padding-top: 100%;"></i-amphtml-sizer>
                    <img alt="Emping" class="i-amphtml-fill-content -amp-fill-content i-amphtml-replaced-content -amp-replaced-content" src="{{ site.baseurl | append:'/assets/photo.png'}}">
                </amp-img>
                <h1 class="name">{{ site.title }}</h1>
            </a>
            <h2 class="description">{{site.description}}</h2>
        </div>
    </div>
</header>
```


* 在`_layouts/default.html`中引用导航代码块:
```
   <!doctype html>
   <html lang="en">
   <!--include 直接包含了_include/head.html的代码-->
   {% include head.html%}
   <body>
    <!--引用导航代码块-->
   {% include header.html %}
   <div class="page-content">
       <div class="wrapper">
           <!--content定义模板中可变内容,引用者进行添加内容-->
           {{ content }}
      </div>
   </div>
   
   </body>
   </html>
``` 


* 添加博客首页,添加`/blog/index.html` ,
    * [页面变量](http://jekyll.com.cn/docs/variables/)如`site.posts`

```
---
layout: default 
title: blog 
--- 
<h1>这是博客主页</h1> 
<h2>未分页的全部博客</h2>
 {% for post in site.posts %}
    <a href="{{ site.baseurl|append: post.url}}">{{post.title}}</a>
 {% endfor %}
 
 
 <h2>分页的博客,每页两个</h2>
 {% for post in paginator.posts%}
    <a href="{{ site.baseurl|append: post.url}}">{{post.title}}</a>
 {% endfor %}
 
 {% if paginator.total_pages>1 %}
     
     {% if paginator.next_page_path %}
        <a href="{{site.baseurl|append:paginator.next_page_path}}">下一页</a>
     {% endif %}
     
     {% if paginator.previous_page_path %}
        <a href="{{site.baseurl|append:paginator.previous_page_path}}">上一页</a>
     {% endif %}
     
 {% endif %}
 ```


* 为每篇博客设置显示样式`_layouts/post.html`,如下

```
---
layout: default
---
<article class="post" itemscope itemtype="http://schema.org/BlogPosting">
    <div class="post-content" itemprop="articleBody">
        {{ content }}
    </div>
</article>
```


* 下面添加几篇博客,命名规则必须是"YYYY-MM-DD-name.MAKEUP"
```
 ├── _posts                           
 |   ├── 2017-03-09-chenfucaijun.md    
 |   └── 2017-03-10-zhangsanlisi.md  
```


* 比如 2017-03-09-chenfucaijun.md 博客内容如下,多复制几篇,修改日期

```
   ---
   layout: post
   title:  "陈府才俊的博客:Jekyll基本介绍"
   date:   2017-03-09 10:59:21 +0800
   ---
   
   
   
   You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run ` bundle exec jekyll serve
   `, which launches a web server and auto-regenerates your site when a file is updated.
   
   To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.md` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.
   
   Jekyll also offers powerful support for code snippets:
   
   
   {% highlight ruby %}
   def print_hi(name)
     puts "Hi, #{name}"
   end
   print_hi('Tom')
   #=> prints 'Hi, Tom' to STDOUT.
   {% endhighlight %}
   
   Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].
   
   [jekyll-docs]: http://jekyllrb.com/docs/home
   [jekyll-gh]:   https://github.com/jekyll/jekyll
   [jekyll-talk]: https://talk.jekyllrb.com/
``` 


* 执行一遍``,预览效果,无样式的情况下,应该是这样的
![Markdown](http://p1.bpimg.com/1949/487e56829c922aa3.png)


* 基本的博客网站已经搭建完成,下面来引用样式,让他变得更美观吧!
* Jekyll支持直接解析sass来渲染样式,必须要放在`_sass`中!
    * 新建`_sass` 文件夹,放入我实现准备好的[两个文件](https://github.com/chenfucaijun/chenfucaijun.github.io/tree/master/_sass):`_img.scss`和`main.scss`

    
* 将`css/mystyle.css`修改为`css/mystyle.scss`,内容修改如下:
     ```
     ---
     ---    
     @import "main";
         
     html {
       height: 100%;
     }     
     body {
       display: flex;
     ```


* 其他一些资源文件,如头像文件放置在了`/assets/photo.png`
* `.gitignore`文件指明需要忽略的文件,内容如下:
```
_site
.sass-cache
Gemfile.lock
*.gem
.idea/
```

* 至此,一个看起来不是那么丑的博客主页搭建完毕



## Github Pages绑定你自己的专属域名
* 首先你要拥有一个域名,比如我的域名是`chenlei.xyz`
![Markdown](http://p1.bqimg.com/576036/620f77074d39541d.png)


* 然后你需要在你的目录下新建一个**CNAME**文件,填写该域名。
```
chenlei.xyz
```


* 然后去找DNS服务器提供商将你的域名解析到[Github Pages主页的IP上](https://help.github.com/articles/setting-up-an-apex-domain/),下面二选一

```
192.30.252.153
192.30.252.154

```

* 我的域名是通过阿里云买的,直接由阿里云提供云解析,
 * 解析设置如下(记录类型A,主机记录@(意指不加www),记录值填写192.30.252.153或者192.30.252.154): 
![Markdown](http://p1.bpimg.com/576036/bf8f39a20c803810.png)


* 设置完毕后,访问`http://chenfucaijun.github.io.`会重定向到`http://chenlei.xyz`




## GET清单:
* 使用Githhub Pages搭建自己的个人主页
* 搭建Jekyll的本地运行环境,运行调试Jekyll工程,引入Gemfile第三方库
* 掌握Jekyll的基本语法和使用方法
    * 遵循Jekyll规范的Github Pages目录结构
    * Jekyll的YAML头、全局变量、配置文件、新建页面、博客撰写和分页
    * Jekyll引用样式(css,scss,js)、图片等资源
* 绑定自己的专属域名到GithubPages中



# 谢谢观看!











