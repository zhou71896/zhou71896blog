---
title: hexo搭建
date: 2017-08-14 14:42:43
tags: hexo
categories: hexo
---
<blockquote class="blockquote-center">简单高效</blockquote>
现在很多朋友都比较喜欢用GitHub来搭建静态网站，原因就是省钱简单。
所以我也利用hexo+github来搭建了该博客，用于分享交流一些心得和体会。
在此将各种操作步骤和一些坑记录在此，以便以后可以使用。


{% note danger %} 
# 准备安装 # 
---
* 下载安装 [node.js](https://nodejs.org/zh-cn/)，自带npm
* 下载安装 [git](https://git-scm.com/)
* 下载安装hexo 方法如下(需要翻墙用 [lantern](https://github.com/getlantern/lantern)) 邀请码：L9F3UZ
{% codeblock lang:java %} npm install -g hexo
{% endcodeblock %} 
{% endnote %}

{% note danger %} 
# 本地搭建hexo静态博客
---
* 新建一个文件夹, blog
* 进入blog的目录, 右击选择运行git, 输入 hexo init (生成hexo模版,可能需要翻墙)
* 如果需要的话，运行npm install
* 最后输入 hexo s (运行程序，访问[地址](https://localhost:400),可以看到本地博客搭建完成)
{% endnote %}

{% note danger %} 
# 博客关联Github
---
* 在Github上创建名字为XXX.github,io的项目,XXX为github额用户名
* 打开本地的blog博客文件夹找到项目配置文件_config.yml,将相关的属性设置如下
{% codeblock lang:java %} deploy:
  type: git
  repository: https://github.com/XXX/XXX.github.io.git
  branch: master
{% endcodeblock %} 
* 运行：npm install hexo-deployer-git –save
* 运行：hexo g（本地生成静态文件）
* 运行：hexo d（将本地静态文件推送至Github）
此刻，打开浏览器访问 https://XXX.github.io
{% endnote %} 

{% note danger %} 
# 绑定域名
---
博客已经搭建好，能够在github的域名商访问，但现在我们需要设置自己的域名并将其绑在我们的这个博客上。
* 域名提供商设置
  添加两条A记录:
  ->192.30.252.154
  ->192.30.252.153
  添加一条CNAME记录:
    CNAME->zhou71896.github.io
* 博客添加CNAME文件
    配置域名解析后，进入博客目录，在source目录下面创建CNAME文件 ，写入域名
* 运行: hexo g
* 运行: hexo d
{% endnote %} 

{% note danger %} 
# 更新博客内容 #
---
 至此博客已经搭建完毕，域名的解析也完成，剩下的问题就是更新内容。
## 更新文章##  
* 在blog文件夹执行: hexo new "my new paper",对应的source->文件夹下会生成.md文件
* 编辑该文件（使用markdown规则）
* 修改初始字段
    * title 文章的标题
    * date 创建日期
    * updated 修改日期
    * comments 是否开启评论true
    * tags 标签
    * categories 分类
* 编辑正文内容(MarkDown)
* hexo clean 删除本地静态文件(当前目录下)
* hexo g 生成金静态文件
* hexo d 将本地静态文件推送址github上面 
{% endnote %} 

{% note danger %} 
## 添加菜单## 
进入theme目录，编辑_config.yml文件,找到menu:字段。
{% codeblock lang:java %} menu:
    home: /
    about: /about
    ......
{% endcodeblock%}
找到anhuages目录，编辑zh-Hans.yml文件:
{% codeblock lang:java %} menu:
    home: 首页
    about: 关于作者
    ......
{% endcodeblock %}
{% endnote %} 

{% note danger %} 
## 文章中插入图片## 
{% codeblock lang:java %} ![/uoload_image/1.jpg]
{% endcodeblock %}
然后进入themes-主题名-source-upload_image目录下(自己创建)，将图片放到这个目录下，就可以了。

说明：当执行hexo g命令时，会自动把图片复制到 public文件的upload_image目录下。
{% endnote %}

{% note danger %} 
# hexo配置本地搜索 #
---
* 要使用本地搜索,先要生成博客索引数据，通过下面这个插件方可:
{% codeblock lang:java %}npm install hexo-generator-search --save
{% endcodeblock %}
* 然后在Hexo 站点 _config.yml中添加如下配置即可:
{% codeblock lang:java %}search:
    path:search.xml
    field:post
{% endcodeblock %}
更多配置说明可以参看:[hexo-generator-search](https://github.com/PaicHyperionDev/hexo-generator-search)
* 然后在  themes/next/layout/_partials/search 目录下修改 localsearch.swig 文件。
原始文件内容如下：
{% codeblock lang:javascript %}
 <script type="text/javascript">
     var search_path = "<%= config.search.path %>";
     if (search_path.length == 0) {
     	search_path = "search.xml";
     }
     var path = "<%= config.root %>" + search_path;
     searchFunc(path, 'local-search-input', 'local-search-result');
 </script>
{% endcodeblock %}
修改后的文件如下
{% codeblock lang:javascript %}
<div class="popup">
 <span class="search-icon fa fa-search"></span>
 <input type="text" id="local-search-input" placeholder="search my blog...">
 <div id="local-search-result"></div>
 <span class="popup-btn-close">close</span>
</div>
{% endcodeblock %}
{% endnote %} 

{% note danger %} 
# 解决分类和标签找不到问题 #
---
* 在根目录下的source文件夹中分别创建categories和tags文件
* 分别在两个文件夹下面创建index.md内容为
    * title: 分类 
    date: 2017-07-22 12:34:33
    type: "categories"
    * title: 标签 
    date: 2017-07-22 12:34:33
    type: "tags"
{% endnote %}






