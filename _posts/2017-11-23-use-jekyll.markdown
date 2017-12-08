---
layout: post
title:  "尝试jekyll与GitHub，问题与解决"
date:   2017-11-23 12:22:25 -0700
categories: Jekyll
---
Ruby零基础，折腾起来jekyll还是有点头疼的。  
此文既是对之前所做工作的总结，也算是测试发一篇文章。准备接下来进一步的设置。

自学尝试建立此Jekyll的过程中，遇到过以下几个问题，通过都解决了。  

[问题1.][p1]  
使用$ jekyll new sitename时，  
报错Could not load Bundler. Bundle install skipped.  
解决方法：运行$ gem install bundler

[问题2.][p2]  
使用$ jekyll serve时，  
报错Error:  Permission denied - bind(2) for 127.0.0.1:4000.  
解决方法：  
使用netstat -ano  
查看各端口被占用情况。  
找到4000端口被占用的PID.  
如：  
协议  本地地址          外部地址          状态           PID  
TCP  127.0.0.1:4000    0.0.0.0:0         LISTENING     3580  
TCP  127.0.0.1:4000    127.0.0.1:2345    ESTABLISHED   3580  

使用Windows任务管理器，选择“Services”栏，通过PID找到FxService，右键-停止。

根据[查到的博文][p2]  
另可在启动jekyll服务的时候指定端口号，如下：  
jekyll serve --port 3000  
输入 http://localhost:3000/ 访问。  

另可在配置文件_config.yml中添加端口号设置（参考官网文档-Serve Command   OptionsPermalink），如下：  
\# port  
port: 1234   
此时，启动jekyll服务后，访问 http://localhost:1234/   

[问题3.][p3]  
GitHub for Windows无法登陆。  
解决方法：更新.NET Framework.

[p1]: http://zhatrix.com/tech/2017-10-28-jekyll-install-and-use/
[p2]: https://gaohaoyang.github.io/2016/03/12/jekyll-theme-version-2.0/
[p3]: https://github.com/gitextensions/gitextensions/issues/2044