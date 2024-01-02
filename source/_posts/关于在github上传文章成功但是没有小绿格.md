---
title: 如何解决在github上成功上传文章但是没有小绿格
date: 2023-10-21 15:58
tags: 
    - 适配性
categories: 
    - 日常问题
---
# 解决日常遇到的问题  
## 在配置github的仓库(repository)时候遇到了几个小问题  
打算自己搭建个自己的blog网站，于是便开始跟着一个大佬的[建站指南开始做](https://nickxu.me/2022/02/13/Hexo%20+%20Butterfly%20%E5%BB%BA%E7%AB%99%E6%8C%87%E5%8D%97%EF%BC%88%E4%B8%80%EF%BC%89Hexo-%E6%A1%86%E6%9E%B6/)  
在将[个人的静态网站](https://stitchk.github.io/)上传到公网上(也就是将我的blog推广到github上)让大家都能访问的过程中,我遇到了以下问题：在`hexo cl&hexo g`没问题后,当我输入`hexo d`的时候出现了下列错误:  
  
![错误1](https://stitch-best.oss-cn-beijing.aliyuncs.com/%E5%87%BA%E7%8E%B0%E7%9A%84%E9%94%99%E8%AF%AF.png)  
-----
于是我便查询各种资料试图寻找是哪里出现的错误  
## 关于密钥  
查询到有可能是密钥部署没成功，我便通过以下手段查看:  
![手段1](https://stitch-best.oss-cn-beijing.aliyuncs.com/%E6%89%8B%E6%AE%B51.png)  
可以看到,上面所出现的You've successfully authenticated已经证明了我的问题不出在密钥上  
## 关于邮箱地址  
接下来是看github和本地user的邮箱地址是否匹配:  
通过输入`git config user.email`查看本地用户的邮箱  
显示结果如下:  

![本地用户邮箱](https://stitch-best.oss-cn-beijing.aliyuncs.com/%E7%94%A8%E6%88%B7%E9%82%AE%E7%AE%B1.png)  
再在github上查看github绑定的邮箱:  
![github邮箱](https://stitch-best.oss-cn-beijing.aliyuncs.com/github%E9%82%AE%E7%AE%B1.png)  
发现两个是一样的，那么问题来了，究竟是哪里的问题呢?因为网上大部分查到的都是因为邮箱不匹配才造成的没有小绿格子的问题，而我的邮箱确实匹配的，这问题也确实卡了我很久  
## 查看`_config.yml`的代码  

在查看`_config.yml`的代码的时候发现在部署(deploy)中仓库(repository)处的地址是http格式的，那么有没有一种可能是因为我直接贴的http格式的网址无法被SSH客户端识别?  
于是我将原来的网址格式从https://github.com/username/repositoryname.github.io改为git@github.com:username/repositoryname.github.io.git，也就是改成了SSH URL  

---  
在重新`hexo cl&hexo g&hexo d`之后惊喜地发现小绿格又出现了!  
![finish](https://stitch-best.oss-cn-beijing.aliyuncs.com/great%20result.png)  

---
总的来说，过程虽然曲折且痛苦，但总还是解决了