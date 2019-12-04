---
title: hosts使用
date: 2016-08-01 18:36:53
tags: 
- hosts
---
<h2>关于hosts二三事</h2>
没有任何的意思，方便程序员查资料！

<h3>原理</h3>
>总的来说，Google配合baidu可以发挥出中文搜索的功力了。百度的优点，常见问题搜索比较全面，一般能找到心仪答案，但是对于较为生僻的问题，一般主要是不准。<br>
使用google一般比较准确，前面的搜索项能代表基本问题。一般配合baidu中文搜索的能力补全。平时不可能一直开着vpn或者shadowsocks。<br>

**p.s.**发现了个好玩的：国外IP访问国内网页，竟然有地域限制，蛤蛤！<br>

>DNS污染（域名污染），将网址解析为不正确的IP地址，使得访问不到正确的IP。但是计算机，实际上是先在本地hosts文件中查看，如果解析出正确的IP，则可以直接访问，不需要访问DNS服务器了。<br>

**p.s.**hosts需要不定期更新（当你上不去的时候）。
<h3>关于修改hosts</h3>
**windows:**C:\Windows\System32\drivers\etc <br>
>目录下的hosts文件，权限问的话，先拷出来，改完后，覆盖回去。最后**cmd**下**ipconfig /flushdns**<br>

**ubuntu:**/etc<br>
>目录下hosts修改。<br>

<!--more-->

**Google使用技巧**

![](http://i.imgur.com/FpgqLx0.jpg)

<h3>经常去的源</h3>
<a href="https://laod.org/hosts/2016-google-hosts.html">laod</a><br>
<a href="https://serve.netsh.org/pub/ipv4-hosts/">奶齿</a>
