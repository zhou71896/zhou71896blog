---
title: hexo写文章
layout: draft
date: 2017-08-15 13:11:04
tags: hexo
categories: hexo
---
<blockquote>简单高效</endblockquote>

上一文章我们已经用hexo搭建起了我们的一个基础的博客框架，接下来我们要开始写自己的文章。
因此今天要和大家分享的是，怎么写文章的一些基础知识。
# 写作 #
----
 创建一篇新的文章
 {% codeblock lang:bash %}$ hexo new [layout] <title>{% endcodeblock %}
 你可以在命令中指定文章的布局{layout},默认为post,可以通过修改_config.yml中的default_layout来指定默认布局。
## 布局（Layout）##
  post    path:   source/_posts
  page    path:   source/pagename
  draft   path:   source/_drafts
## 文件名称 ##
  Hexo会以默认的标题作为文件名称,但你可以编辑new_post_name参数来改变默认的文件名称。
## 草稿 ##
  草稿是hexo的一种特殊布局:draft,这种布局在建立时会被保存到 source/_drafts 文件夹，你可以通过publish命令将草稿移动到source/_posts文件夹，该命令与 new 类似，你也可以在命令行中指定 layout 来布局。
``` bash
$ hexo publish [layout] <title>
```
  草稿不会默认显示在页面中，你可以在执行时加上 --draft 参数,或是把render_drafts参数设为 true 来预览草稿。 
## 模版（Scaffold）##
在新建文章时，Hexo会根据scaffolds文件夹内对应的文件来创建文件，例：
```bash
$ hexo new photo "My Gallery"
```
在执行这行命令的时候，Hexo会尝试在Scaffold文件夹中寻找photo.md，并根据其内容建立文章。
## Front-matter ##
Front-matter 是文件最上方---分割的区域用于指定个别文件变量的：
```bash
title: Hello World
date: 2010/7/13
```
## 标签插件(TagPlugin) ##
标签插件和Front-matter中的标签不同，它们是用户在文章中快速插入特定内容的插件
## 引用块 ##
在文章中插入引言，可包含作者，来源和标题。更多资料可以查看[详细资料](https://hexo.io/zh-cn/docs/tag-plugins.html)
