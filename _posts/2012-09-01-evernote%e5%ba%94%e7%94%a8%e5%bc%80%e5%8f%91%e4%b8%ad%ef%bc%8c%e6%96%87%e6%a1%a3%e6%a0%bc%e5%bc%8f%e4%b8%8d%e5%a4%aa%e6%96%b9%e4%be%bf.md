---
title: 'Evernote应用开发中，文档格式不太方便&#8230;'
author: richard
layout: post
permalink: /2012/09/01/evernote%e5%ba%94%e7%94%a8%e5%bc%80%e5%8f%91%e4%b8%ad%ef%bc%8c%e6%96%87%e6%a1%a3%e6%a0%bc%e5%bc%8f%e4%b8%8d%e5%a4%aa%e6%96%b9%e4%be%bf/
dsq_thread_id:
  - 4414113676
categories:
  - 代码
---
为了某些邪恶的想法，我决定用evernote的API把所有note导入本地处理。结果今天的时间几乎都花在了这个上面&#8230;虽然最终成功的把文章导出，但是同时发现了个很严重的问题：原以为evernote用html/xml直接给抓取的网页编码。结果没成想，note扒下来之后才发现，人家evernote用的是自己的enml格式（就是把xml的x改成evernote缩写&#8230;）。于是乎，各种浏览器纷纷表示无能为力。上网查询，evernote的工程师<del datetime="2012-09-01T12:37:46+00:00">不知到什么时候</del>说<del datetime="2012-09-01T12:37:46+00:00">的</del>目前还没有开发服务器端的格式转换API&#8230;瞬间傻眼了。下面先写个总结：

说到evernote的app开发，首先可以参考官网的dev page。在开发页面中，有evernote的整体开发流程介绍：

### <img class="alignnone" title="流程介绍" src="http://ww1.sinaimg.cn/mw690/65c83a2bgw1dwhbme710jj.jpg" alt="" width="690" height="186" />

注册api key，下载SDK，然后再在sandbox里面注册一个新账户。就可以开发啦～lol<!--more-->

  
把下载的SDK解压，然后运行EDAMTest.py，注意：EDAMTest.py代码中需要填入developer token（而不是api key&#8230;）。注册developer token的地址：https://sandbox.evernote.com/api/DeveloperToken.action  
执行结束，得到正确结果：  
<code width='570'>&lt;br />
fnl@fnl-OptiPlex-790:~/evernote-sdk-python/sample$ python EDAMTest.py&lt;br />
Is my Evernote API version up to date? True&lt;/p>
&lt;p>Found 1 notebooks:&lt;br />
* zhaoweichen 的笔记本&lt;/p>
&lt;p>Creating a new note in the default notebook&lt;/p>
&lt;p>Successfully created a new note with GUID: 3f6e1c19-54bd-48b7-ba59-b16589c7c8bb&lt;br />
</code>  
随后，就可以参照evernote的API参考手册来编写APP了～最后，虽然贴做出来的代码并没有达到搞定HTML文档的效果，至少也可以把所有文档下载下来。就贴在最后吧。

<div>
</div>

<code lang='python' height='960' width='570'>&lt;br />
import sys&lt;br />
import hashlib&lt;br />
import binascii&lt;br />
import time&lt;br />
import thrift.protocol.TBinaryProtocol as TBinaryProtocol&lt;br />
import thrift.transport.THttpClient as THttpClient&lt;br />
import evernote.edam.userstore.UserStore as UserStore&lt;br />
import evernote.edam.userstore.constants as UserStoreConstants&lt;br />
import evernote.edam.notestore.NoteStore as NoteStore&lt;br />
import evernote.edam.type.ttypes as Types&lt;br />
import evernote.edam.error.ttypes as Errors&lt;/p>
&lt;p>authToken = "填写你的developer token～"&lt;br />
evernoteHost = "sandbox.evernote.com"&lt;br />
userStoreUri = "https://" + evernoteHost + "/edam/user"&lt;/p>
&lt;p>userStoreHttpClient = THttpClient.THttpClient(userStoreUri)&lt;br />
userStoreProtocol = TBinaryProtocol.TBinaryProtocol(userStoreHttpClient)&lt;br />
userStore = UserStore.Client(userStoreProtocol)&lt;/p>
&lt;p>versionOK = userStore.checkVersion("Evernote EDAMTest (Python)",&lt;br />
                                   UserStoreConstants.EDAM_VERSION_MAJOR,&lt;br />
                                   UserStoreConstants.EDAM_VERSION_MINOR)&lt;br />
print "Is my Evernote API version up to date? ", str(versionOK)&lt;br />
print ""&lt;br />
if not versionOK:&lt;br />
    exit(1)&lt;/p>
&lt;p>noteStoreUrl = userStore.getNoteStoreUrl(authToken)&lt;br />
noteStoreHttpClient = THttpClient.THttpClient(noteStoreUrl)&lt;br />
noteStoreProtocol = TBinaryProtocol.TBinaryProtocol(noteStoreHttpClient)&lt;br />
noteStore = NoteStore.Client(noteStoreProtocol)&lt;/p>
&lt;p># List all of the notebooks in the user's account&lt;br />
notebooks = noteStore.listNotebooks(authToken)&lt;br />
print "Found ", len(notebooks), " notebooks:"&lt;br />
for notebook in notebooks:&lt;br />
    print "  * ", notebook.name&lt;br />
    print "    notebook: ",notebook&lt;br />
    print "    guid    : ",notebook.guid&lt;/p>
&lt;p>print "another try"&lt;/p>
&lt;p>filter = NoteStore.NoteFilter()&lt;br />
filter.notebookGuid = notebook.guid&lt;br />
noteList = noteStore.findNotes(authToken,filter,0,10) #only matadata&lt;br />
for n in noteList.notes:&lt;br />
    print n.title, n.guid&lt;br />
    content = noteStore.getNote(authToken, n.guid, True, False, False, False)&lt;br />
    fileHandle = open ( n.title + '.enml', 'w' )&lt;br />
    fileHandle.write ( content.content )&lt;br />
    fileHandle.close()&lt;br />
</code>  
其实，enml格式的问题也不是没有解决方法啦～就是会比较曲线：用evernote的邮件转发API转发至邮箱，然后再从邮箱里面抓取HTML代码&#8230;同样的，这么做是需要python支持IAMP邮箱登录等功能。好在有牛逼闪闪的库文件在。废话不多说，直接上代码～  
<code lang='python' width='570'>&lt;br />
import imaplib&lt;br />
import email&lt;br />
import StringIO&lt;/p>
&lt;p>gmail_user = 'your email address'&lt;br />
gmail_pass = 'your password'&lt;br />
M = imaplib.IMAP4_SSL('imap.gmail.com')&lt;br />
M.login(gmail_user, gmail_pass)&lt;br />
M.select()&lt;br />
fileHandle = open ( 'subject.html', 'a' )&lt;br />
typ, data = M.search(None, 'ALL')&lt;br />
for num in data[0].split():&lt;br />
    typ, data = M.fetch(num, '(RFC822)')&lt;br />
    tempMessage = StringIO.StringIO(data[0][1])&lt;br />
    msg = email.message_from_file(tempMessage) #parsing&lt;br />
    subject = msg.get("Subject")&lt;br />
    h = email.Header.Header(subject)&lt;br />
    dh = email.Header.decode_header(h)&lt;br />
    subject = dh[0][0]&lt;br />
    print "subject:", subject&lt;br />
    fileHandle.write ( subject )&lt;br />
fileHandle.close()&lt;br />
M.close()&lt;br />
M.logout()&lt;br />
</code>  
这段代码的功能比较简单，就是登录进邮箱，然后搞到邮件，再然后把标题取出来打印到文件。（还是要赞python一个，这样的功能用不到30行代码就可以搞定～）至于具体的eml格式转换，还没写完，就不贴上来了。  
关于登录，可能有的童鞋会认为直接把用户名密码写进代码不好，下面是另一种登录的方法，需要每次执行的时候都输入用户名、密码。这样的设计很适合在工程完成之后的实际使用。不过，测试的时候，还是上面那样比较省事～  
<code lang='python' width='570'>&lt;br />
M.login(getpass.getuser(), getpass.getpass())&lt;br />
</code>