---
title: '[CodeAudit] SQL Inject 0'
date: 2018-07-29 08:56:51
tags:
 - websecurity
 - CodeAudit
 - BasicKnowledge
categories: InformationSecurity
index_img: https://i.loli.net/2018/07/29/5b5d121f21f3d.png

---
# 前言
  SQL注入（SQL Inject），定义我就不多说了，这里是[百度百科](https://baike.baidu.com/item/SQL注入)。
  原理很好理解，但是想掌握却是不简单，需要练习与实战，望大家不要犯像我一样眼高手低、自以为是的病。
  下面开始进入正题。
# 简单例子
首先从PHP开始。一个最经典的例子：
> login1.php
```
$sql = "select * from user where name='".$name ."' and passwd='".md5($passwd)."'"; //重点在这里，这句是将sql语句拼接，语句的作用是从数据库里查找提交的用户名密码是否存在
$stmt = $dbh->query($sql); // 执行上句的sql语句
```
关键代码就是那个拼接语句，这就是sql注入的源头。
我们输入payload：
> admin' --&nbsp;

将这句输入到账号输入框（注意在--后面有个空格，如果没有空格就不会成功），然后密码随意输入。结果如下：
![将payload输入到账号的位置](https://i.loli.net/2018/07/29/5b5d5b702ce1e.png "将payload输入到账号的位置")
![成功登陆](https://i.loli.net/2018/07/29/5b5d5bf616885.png "成功登陆")
这就是传说中的万能密码，这种漏洞可以以任意用户名登陆而不需要知道密码。附：[万能密码](https://www.cnblogs.com/Downtime/p/7648182.html)
不过呢，毕竟这是很简单的漏洞，现在已经很少很少能遇到这种漏洞了。
下面在看另一个例子：
```
$sql = "select * from info where uid=".$id; //关键语句，依然是拼接导致的漏洞。此语句是根据id查询用户信息
$stmt = $dbh->query($sql); // 执行上句的sql语句
$result = $stmt->fetchAll(PDO::FETCH_ASSOC); //将结果由对象转换为数组，便于使用

$sql2 = "select * from user where id=".$id; //同上，这句是查询用户名
$stmt2 = $dbh->query($sql2);
$result2 = $stmt2->fetchAll(PDO::FETCH_ASSOC);
```
```
<div class="card_class card text-white bg-primary mb-3" style="max-width: 18rem;">
    <div class="card-header"><?=$result2[0]['name'];?></div>
    <div class="card-body">
        <h5 class="card-title"><?=$result[0]['phone'];?></h5>
        <p class="card-text"><?=$result[0]['address']?></p>
    </div>
</div>
```
依然是拼接导致的漏洞，只不过不同的表现形式。仔细看代码可以发现，这次的问题是在id这里（本来想写一个灰常简单注入，但是写完发现QAQ）。
看下面的那段代码，由于是只显示一条，而且是固定字段的，所以不会有回显，也不会有报错，所以只有盲注。（如果有人发现其他注入方式可以在评论里留言，一起交流）
下面看下sqlmap跑出来的结果：
![sqlmap结果](https://i.loli.net/2018/07/29/5b5dcba58ee1a.png "sqlmap结果")
盲注呢就是没有待回显的直观，并且效果会弱一点，但是就sql注入而言，依然是很严重的问题。
看过两个例子之后我来总结一下，这是两个很典型很基础的例子，就是因为用户可控的变量，没有经过验证和过滤，直接拼接到sql语句中，造成的问题。
所以从审计的角度来说，凡是用户可控的变量，涉及到sql语句，都是可能会产生sql注入的（其实不止sql注入，只不过本文讲的是sql注入，其他漏洞另说）。
深挖一下漏洞产生的原因：程序员写代码的时候，很少会从安全的角度来考虑，只会从实现功能和性能优化方面考虑，至于不考虑安全性的原因有很多，包括程序员基数大、没有系统的培养学习安全意识、很多非科班出身等，所以不论是从以前还是现在（就sql注入来讲，现在的程序员知道防护的比例会提高很多，得益于这么多年sql注入的各种发展= 。=）。
至于修复么，简单一句话讲就是过滤危险字符或使用orm的预编译。详细的后面讲。
sql注入的原理是不复杂，理解起来也很简单。但是理解不代表会用，而且这也只是简单的一些，后面我会尽量多的收集各种案例，这样会更扎实的掌握一种漏洞。注意，理解原理并不代表掌握这种漏洞，各种场景和各种产生情况都是需要扎实的基本功，而掌握漏洞就是代码审计的基本功。从一只代码审计的菜鸟开始，或许明天就是一只大菜鸟~
## 备注
如果看上面的sql看不懂，那么就说明需要学习基础的sql语法，这个推荐大家百度or谷歌关键字：sql语法。
善用搜索引擎，这是一项通用技能，也可以说是一项必备技能。使用搜索引擎的好处也就不多说了，大家自行体会。
# 书籍推荐
作为第一期，推荐大家一本重量级的书，也是我最近在看的书：
[《深入理解计算机系统》](http://product.dangdang.com/24106647.html)
如果经济能力足够，推荐大家买正版书。
[百度云](https://pan.baidu.com/s/1KpMLl77fvthgzypapy5inA "e2ec")（e2ec）
