---
title: Evernote开发：有关EnailNote的API
author: richard
layout: post
permalink: /2012/09/08/evernote%e5%bc%80%e5%8f%91%ef%bc%9a%e6%9c%89%e5%85%b3enailnote%e7%9a%84api/
dsq_thread_id:
  - 4433201245
categories:
  - 代码
---
虽说Evernote的API给的比较简单易用，但还是存在诸多问题。首先就是数据导出方面的问题。与网页文件的HTML格式不同，Evernote使用的是自家的enml数据格式。这就使得导出的时候出现一些问题：数据格式不通用。不但不通用，在API中还没有给出格式转换的工具。但是说实话，拥有独特的数据格式本应不是什么大问题。只是对于我这样的小开发者来说，这样的设置显然是大大降低了易用度。

话说回来，之前看到，Evernote论坛上，他们的工程师（好象是）说如果想做到数据格式转换，那么最好还是通过E-mail转发Note的方式来完成。<del datetime="2012-09-08T01:06:46+00:00">但是一旦接受了这样的设定</del>无奈之下，我做了Gmail邮件的抓取和解析（代码在之前的文章里有贴出来）。万事具备，于是我开始测试官网上提供的EmailNote这个API。结果，真正坑爹的BUG出现了&#8230;

写出来的代码完全没法用，Evernote一直报错，错误类型还是针对我Developer Token的“PERMISSION_DENIED”。上网查询，在Evernote的官网论坛上也找到一段<a title="Problem sending email" href="http://discussion.evernote.com/topic/23907-emailnote-returns-errorcode-permission-denied/" target="_blank">对话</a>，讨论的正是我遇到的问题。Evernote的人说到先是“ The emailNote function **only works with a client key** but not with a oAuth key”，然后又说“**Client keys aren&#8217;t available anymore** (<a title="External link" href="http://blog.evernote.com/tech/2012/04/24/security-enhancements-for-third-party-authentication/" rel="nofollow external">learn why here</a>) and third party application **cannot access that functionnality anymore**.”  
<!--more-->

  
泥马，API改成自家用之后还放出来招摇过市&#8230;不过好在Evernote的人回复说“We are continually working on improving our documentation and **this will be taken care of very soon**”，只是两个多月已经过去了，这API还是不能用。