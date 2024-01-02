---
title: Block Cipher-AES
date: 
tags: Block Cipher
categories: 
    - Applied Cryptography  
    - Class
--- 

# AES算法加密简介

## 什么是AES  

AES是高级加密标准，在密码学中又称Rijndael加密法，是美国联邦政府采用的一种区块加密标准。这个标准用来替代原先的DES，目前已经被全世界广泛使用，同时AES已经成为对称密钥加密中最流行的算法之一。AES支持三种长度的密钥：128位，192位，256位。  

## AES加密流程  

对称加密解密流程:  

![20231225134436](https://stitch-best.oss-cn-beijing.aliyuncs.com//20231225134436.png)  


AES加密解密基本流程：  

![20231225134619](https://stitch-best.oss-cn-beijing.aliyuncs.com//20231225134619.png)  

对于128位密钥的加密以及解密都是十轮的，相当于跑个轮函数，但是第10轮跟第1-9轮不一样。加密的第1轮到第9轮的轮函数一样，包括4个操作：字节代换、行位移、列混合和轮密钥加。最后一轮迭代不执行列混合。另外，在第一轮迭代之前，先将明文和原始密钥进行一次异或加密操作。  

tips:当密钥长度不一样的时候加密轮次也不一样，AES（高级加密标准）是一种对称加密算法，它支持128位、192位和256位三种密钥长度。加密和解密的轮次取决于密钥长度：

对于128位密钥：

加密轮次：10轮 解密轮次：10轮
对于192位密钥：

加密轮次：12轮 解密轮次：12轮
对于256位密钥：

加密轮次：14轮  解密轮次：14轮

# AES具体加密流程  

1. 给定一个明文M，将State初始化为M，并将轮密钥与State进行异或操作(AddRoundKey);  

2. 在加密的第一轮到第N-1轮中，每一轮都对其先进行字节替换(SubBytes),对替换的结果State做行移位操作(ShiftRows)，然后再对State做列混淆变换（列混合变换）操作(MixColumns)，然后再进行轮密钥加操作(即轮密钥与State异或，AddRoundKey);  

3. 在最后一轮中依次进行SubBytes、ShiftRows和AddRoundKey操作，无需进行MixColumns操作;  

4. 结果中的State便是密文C。  

## 轮函数中的操作  

### 字节替换变换(SubBytes)  

字节替换操作使用一个S-盒对State的每个字节都进行独立的替换，S-盒如下：  

![20231225141457](https://stitch-best.oss-cn-beijing.aliyuncs.com//20231225141457.png)  

字节替换属于非线性替换，具体原理就是通过一个替换表（S盒）对每个字节进行替换，实际上就是一个查表操作，并且此过程可逆，将每一个字节的前4位作为行值，后4位作为列值，去S盒查找，进行输出。  
例如字节为0x14，转换为二进制为0001 0100,那么前四位的16进制为1，后四位的16进制为4，去查找s盒中的第1行第4列的值，可以看出为0xfa，就把原先的字节0x14替换为0xfa。    

### 逆字节替换(InvSubBytes)  
解密过程与加密过程类似，但是用的是逆S-盒  
逆S-盒:  

![20231225160256](https://stitch-best.oss-cn-beijing.aliyuncs.com//20231225160256.png)

### 行移位变换(ShiftRows)  
行移位是一个简单的左循环移位操作。当密钥长度为128比特时，状态矩阵的第0行左移0字节，第1行左移1字节，第2行左移2字节，第3行左移3字节，如下图所示：  

![20231225151135](https://stitch-best.oss-cn-beijing.aliyuncs.com//20231225151135.png)  

### 行移位的逆变换(InvShiftRows)
行移位的逆变换是将状态矩阵中的每一行执行相反的移位操作，以上图为例，矩阵的第0行右移0字节，第1行右移1字节，第2行右移2字节，第3行右移3字节。  

### 列混合变换(MixColumns)  

![20231225153259](https://stitch-best.oss-cn-beijing.aliyuncs.com//20231225153259.png)  

![20231225153319](https://stitch-best.oss-cn-beijing.aliyuncs.com//20231225153319.png)  

![20231225153648](https://stitch-best.oss-cn-beijing.aliyuncs.com//20231225153648.png)
  
![20231225153548](https://stitch-best.oss-cn-beijing.aliyuncs.com//20231225153548.png)  

### 列混合变换的逆变换(InvMixColumns)  

![20231225160502](https://stitch-best.oss-cn-beijing.aliyuncs.com//20231225160502.png)  

### 轮密钥加(AddRoundKey)  

轮密钥是原来的密钥经过密钥编排算法得到的一个密钥，其长度与明文分组长度相同——16字节、128位，AES中，每一轮迭代的轮密钥都互不相同。

所谓轮密钥加，就是简单地将待加密的内容与轮密钥按位异或。也可以视为字节之间的操作，如下图所示：左边是待加密的内容，右边是轮密钥，等号右边为结果。  

![20231225155413](https://stitch-best.oss-cn-beijing.aliyuncs.com//20231225155413.png)  

轮密钥加参考自:<https://zhuanlan.zhihu.com/p/360393988#:~:text=%E5%AF%86%E9%92%A5%E6%89%A9%E5%B1%95%E7%94%A8%E6%9D%A5%E5%B0%86%E5%8E%9F,%E8%BD%AE%E8%BF%AD%E4%BB%A3%E7%9A%84%E8%BD%AE%E5%AF%86%E9%92%A5%E3%80%82>  

密钥扩展方法也可参考:<https://zhuanlan.zhihu.com/p/360393988#:~:text=%E5%AF%86%E9%92%A5%E6%89%A9%E5%B1%95%E7%94%A8%E6%9D%A5%E5%B0%86%E5%8E%9F,%E8%BD%AE%E8%BF%AD%E4%BB%A3%E7%9A%84%E8%BD%AE%E5%AF%86%E9%92%A5%E3%80%82>  

### 轮密钥加的逆运算(InvAddRoundKey)  

轮密钥加的逆运算同正向的轮密钥加运算完全一致，这是因为异或的逆操作是其自身。