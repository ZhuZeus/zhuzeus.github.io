---
layout: post
title:  Gradle如何将aar发布至Jcenter
author: Joey - 朱勇军
---

如果你做过第三方sdk开发，一定会对包的更新迭代叫苦不迭. 每次版本的更新都需要重新发邮件，要是有个类似Maven的仓库供我们使用，岂不是能够省掉很多发邮件的时间. 于是在我们的Android Studo中，Jcenter由此应运而生. 接下来我们一步一步的解析，看看如何来实现吧.

&emsp;&emsp;&emsp;&emsp;     
                                                        
###  Bintray有关设置
-------

 * 什么是Jcenter
  
    Jcenter 是Jfrog Bintray的一个Maven仓库，用来存放一些更新包。谷歌很多支持包也都放在这个仓库里面.[点这里](http://jcenter.bintray.com/)可以看仓库地址。所以想使用Jcenter服务，需要注册Bintray账号并拿到key(key是啥后面介绍).  
 
 * 申请[Bintray账号](https://bintray.com)
 
    需要注意的是，进入下载页会出现下图两种注册模式,如果使用 **图(一)** 方式注册,在打包的时候可能会出现因为找不到仓库 出现 'http/1.1 404 [Repo not found]' 的异常. 推荐使用第二种 for_source_plan 方式注册.
   
   **图(一)**
   ![](/images/jcenter/for_free_trail.png) 
   
   **图(二)**
   ![](/images/jcenter/for_open_source.png)  
  
   ```
   图一注册是 for_free_trail 模式,图二注册是 for_open_source 模式. 官方文档解释：
   
      If you are on the open source plan and have not yet created an 
   organization then your user profile page will be displayed. 
           
      Either way, you can access your personal profile page, or the 
   profile page of any other organization you own from the profile menu 
   in Bintray’s top ribbon
   ```
   
   更重要的一点，那个 **图(一)** 方式创建的账号，是有试用期的!!30天试用期，鬼知道30后会发生什么...
   
   > 注：如果使用第三方账号登录 如 Github 账号，Google账号，推特账号，默认是按照图一方式注册，可能出现找不到仓库的情况；
        在按照第二种方式注册时,如果填写的内容不符合Bintray规范会出现点击 'Create Account' 无反应. 比如填写邮箱**Gmail**的邮件地址是可以创建的,但如果你用 **QQ邮箱** **163邮箱** (其他邮箱没有测试)是没有反应的。
         
 * 登录Bintray网站,拿到ApiKey
   
     如果你是 for_free_trail 方式注册的账号，你的账号下拉框是这样的:
     
     **图(三)**  
     ![](/images/jcenter/for_source_profile.png) 
     
     这种方式在打包的时候出现了上面说的错误，故在弄不懂的情况下，先不对它作介绍了，着重看**for_soure_open**方式:
    
     **图(四)**  
     ![](/images/jcenter/for_free_profile.png)
     
     点击**Edit Profile**,进入编辑页面,点击 API Key,点击 Show 即可拿到 API Key 了：
     ![](/images/jcenter/api_key.png)

&emsp;&emsp;&emsp;&emsp;  
                                                           
###  配置Android项目，开始编写脚本
-------