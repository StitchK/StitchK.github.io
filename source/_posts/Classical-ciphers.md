---
title: Classical ciphers
date: 
tags: Caesar cipher
categories: 
    - Applied Cryptography  
    - Class
--- 

# 凯撒密码(Caesar cipher)  

## Conception  

在密码学中，恺撒密码(Caesar cipher)，或称恺撒加密、恺撒变换、变换加密，是一种最简单且最广为人知的加密技术。它是一种替换加密的技术，明文中的所有字母都在字母表上向后（或向前）按照一个固定数目进行偏移后被替换成密文。例如，当偏移量是3的时候，所有的字母A将被替换成D，B变成E，以此类推。这个加密方法是以罗马共和时期恺撒的名字命名的，当年恺撒曾用此方法与其将军们进行联系。  
恺撒密码通常被作为其他更复杂的加密方法中的一个步骤，例如维吉尼亚密码。恺撒密码还在现代的ROT13系统中被应用。但是和所有的利用字母表进行替换的加密技术一样，恺撒密码非常容易被破解，而且在实际应用中也无法保证通信安全。   

## Algorithm  

凯撒密码的算法很简单，简单来说就是单表代换，是根据偏移量来替换明文，基本思想是：通过把字母移动一定的位数来实现加密和解密，明文中的所有字母会在字母表中根据偏移量来往前或往后几位。  
举例来说，如果偏移量是5，那么我的明文假设是"Hello World!" 就会替换成"Mjqqt Btwqi!"(当字母往后移的偏移量使得超过了z，那么会循环到头部的a，即mod26)  

以下算法代码参考自:<https://blog.csdn.net/weixin_47585015/article/details/109853825>  

![20231224152357](https://stitch-best.oss-cn-beijing.aliyuncs.com//20231224152357.png)  

# 古典密码中的移位变换以及仿射变换  

## 移位变换

Encryption algorithms : ![20231224155136](https://stitch-best.oss-cn-beijing.aliyuncs.com//20231224155136.png)  

Decryption algorithm : ![20231224155228](https://stitch-best.oss-cn-beijing.aliyuncs.com//20231224155228.png)

## 仿射变换  

Encryption algorithms : ![20231224154811](https://stitch-best.oss-cn-beijing.aliyuncs.com//20231224154811.png)  

Decryption algorithm : ![20231224154847](https://stitch-best.oss-cn-beijing.aliyuncs.com//20231224154847.png) 

Condition : ![20231224155009](https://stitch-best.oss-cn-beijing.aliyuncs.com//20231224155009.png)  