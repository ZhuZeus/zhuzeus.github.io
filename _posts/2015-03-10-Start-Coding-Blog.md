---
layout: post
title:  GitHub Pages + Jekyll 搭建个人免费博客
author: Joey - 朱勇军
---

```
  · MAC环境下搭建jekyll本地环境
  · 将本地jekyll博客托管至github
  · Markdown + jekyll语法简介
  · 快速开始博客（代码详解）
  · 如何自己开发博客模板
```


&emsp;&emsp;&emsp;&emsp;

### 搭建步骤简介
------

 + 首先需要创建一个github私人仓库username.github.io(这个将是你的博客域名)。
 
 + 可以Setting中的Github Pages 栏中选择想要的主题，便会在你之前的空仓库中生成模板代码,即jekyll模板代码(github pages提供主题样式单一,不推荐).
 
   ![theme](/images/choose_theme.png)
   
 + 推荐选择其他的[主题](http://jekyllthemes.org/),我们只需将主题下载下来后稍作修改(如何修改后续介绍)。
 
 + 为方便调试修改，我们需要开始学习[jekyll基础语法](http://jekyllcn.com/docs/installation/ "jekyll中文网").
 
&emsp;&emsp;&emsp;&emsp;

### Mac搭建Jekyll本地环境
-------
 
* jekyll是什么？

​     &emsp;&emsp;&emsp;&emsp;&emsp;jekyll是种简单的标记语言.因为其没有数据库(自然也没有了评论功能),不需要迭代的特性经常用来编写静态博客网站. 其优势在于不需要写html语言,因此能更多的把焦点放在博文编写中.
 * 搭建本地调试环境
   
   &emsp;&emsp;
   
  1, [安装gem](https://rubygems.org/pages/download#formats)(如果没有安装Rubygems).
   
   ![theme](/images/rubygems.png)
   
   &emsp;&emsp;
   
  2, 通过RubyGems安装jekyll,打开终端输入以下命令:
  
    $ gem install jekyll    
      
   &emsp;&emsp;&emsp;&emsp;需要注意的是,githubpages的版本有可能和你本地版本不一致,导致本地能够跑但是 &emsp;&emsp;&emsp;&emsp;github出错.这时需要执行:
     
    $ jekyll --version
    $ gem list jekyll
      
   &emsp;&emsp;&emsp;&emsp;对比gem 中的jekyll和本地jekyll版本检查是否为最新版本.更新Jekyll：
 
    $ gem update jekyll  
      
   &emsp;&emsp;&emsp;&emsp;在下载jekyll的时候，终端刚开始没有进度条显示，请耐心等待。如遇到问题,可在&emsp;&emsp;&emsp;&emsp;  [jekyll github社区](https://github.com/jekyll/jekyll/issues/new)发布Issues.
      
   &emsp;&emsp;
      
  3, 将你下载或者github生成的jekyll主题用编辑器(编辑器如：[Atom](https://atom.io/),[sublime](http://www.sublimetext.com/),[WebStorm](http://www.jetbrains.com/webstorm/))打开,开始本地调试:
     
      $cd to_your_project_path
      $jekyll build
      $jekyll serve
      
  执行下面代码启动jekyll可以无需每次build，jekyll会自动发布到本地服务器，只需要刷新页面即可。但是jekyll全局文件_config.yml改变是需要重新 build的.
  
      $jekyll serve -watch
         
  如果没有错误，即可点[这里](http://localhost:4000)看到效果.如有启动报错，仔细查看jekyll输入日志，问题比较好解决，无需害怕。
      
   &emsp;&emsp;   
      
  4，启动的页面是主页面的index.html,一般的博客主页面会有如下代码(显示博文的主页):
     
   ![theme](/images/code.png)
     
   这段代码的意思是:首先在头文件中加载defaut.html(_layout文件中),按时间倒叙遍历_posts全部文章,读取post中定义的标题和文章，显示在主页. 看到这儿，如果对jekyll的site和post对象不了解，先看看[这个](http://jekyllcn.com/docs/variables/).
   
   
 &emsp;&emsp;&emsp;&emsp;
 
##### 将主题发布到Github Pages
------
   
   注： 主题是github中生成省略，仓库中已有代码，可跳过此操作进行下一步.
  
 * 将代码上传至github pages 专用仓库
  
   1， 进入代码存放路径:
    
       $cd your_project_path
   
   2, 初始化仓库，将本地仓库和远程仓库关联，并将代码提交到master分支
     
       $git init //初始化仓库
       //关联远程仓库,remote-url为远程仓库链接
       $git remote add origin remote-url 
       $git add . 
       $git commit -m “提交文件，添加描述” 
       //将本地分支与远程分支关联
       $git branch --set-upstream local-branch origin/remote-branch 
       $git push
     
      将本地**master**分支文件提交到远程**master**中. 注意,如果是username.github,io域名的博客，都只能在master分支.
  
 * 访问你github的远程地址试试吧.
   
   1, 远程地址默认为username.github.io,在Setting中可查看，其他格式的域名将不能被 &emsp;&emsp;&emsp;&emsp;通过.如果错误，github会发邮件通知.<br>
  
   2, 你也可以第一时间在Setting中查看结果.<br>
  
   3, 也可以来看看github的[异常收集](https://help.github.com/articles/troubleshooting-github-pages-builds/)
    
&emsp;&emsp;&emsp;&emsp;
   
### 写篇博客试试水
-----
  
   * MarkDown简介
     
      由于_post文件中文件按照.md格式编写，有必要熟悉markdown语法。markdown是一种适合在网络上编辑的语言，便于在各种博文中编辑修改文字，链接，图片等. MarkDown是一种书写格式，最终在网页中显示还是会解析成HTML语言。
     
   * MarkDown编辑器
     
     目前有很多的MarkDown的编辑器，推荐几个自己用的. 之前推荐过的 Atom, WebStorm都可以支持markdown编辑. 比较轻量级的编辑：[Typora](http://www.typora.io/)比较推荐，不同的编辑器对于markdown的兼容性不一样，导致同份md文件每个地方显示不一致，以网页中显示为准.
     
   * 初识MarkDown
     
      1, 一些比较常用的特殊符号
       
         > , *,-,+,#,##,###...,```,**a**，--- 比较简单的字符格式编辑,可以
         在md文件编辑器中试试效果，不一一介绍。
       
      2，如何定义超链接.
        
         按照格式[点这里](http://www.baidu.com),即可；[]中写入需要进行超链接
         的文字，后面的()中放入超链接地址。
        
      3，如何插入图片.
         
         ![图片中显示的文字](path) 即可显示图片. ! 表示是图片,[]中显示的是图片
          的文字，可不写. ()中可以写放在工程文件下面的相对路径，也可以是网上的绝
          对路径.
         
          需要注意的是，插入图片为了显示更好看，最好换行插入,将插入图片标记语言单
          独一行.
       
      4，以上介绍大概了解了markdown吗？[这里](http://www.appinn.com/markdown/#blockquote)可以看到更详细的md语法.         
   
   * 调试并发布文章
        
       需要注意的是，_post中的文章必须是xxxx-xx-xx-titile (年-月-日-名称命名) 然后
       在本地调试通过jekyll本地服务器在 http://localhost:4000 (默认地址,一次只能启
       动一个端口，否则会端口冲突，需要更换启动端口)在网页中查看效果,提交到github的m-
       aster分支，等待处理即可。
         
   * 踩过得坑：
         
      1，不同的md编辑器显示的解析后格式都是不同的，在github上次后，需要确认效果无误
           
      2，在github pages的md语法中，特殊符号的上一行和下一行不能有内容，否则当做正常符号；
           
      3，---要在最左边，否则将没有分割线效果；
      
      4, 不要忽视书写博客时的缩进,这将很大程度影响解析格式,尽量按照文章应该的排版格式书写,中文标点应该尽量避免.
      
### 自己动手写主题
------    
      
    