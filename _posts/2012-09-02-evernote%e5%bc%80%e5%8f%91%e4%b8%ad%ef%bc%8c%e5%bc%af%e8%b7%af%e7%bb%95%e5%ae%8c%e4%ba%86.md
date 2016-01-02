---
title: 'Evernote开发中，弯路绕完了&#8230;'
author: richard
layout: post
permalink: /2012/09/02/evernote%e5%bc%80%e5%8f%91%e4%b8%ad%ef%bc%8c%e5%bc%af%e8%b7%af%e7%bb%95%e5%ae%8c%e4%ba%86/
categories:
  - 代码
---
今天把enml到html的转换做完了。其实，重点也只有邮件的接收，还有解码的过程。目前的效果是：通过evernote邮件转发的功能将笔记发送到指定邮箱，然后再用python脚本把邮件下下来&decode。最终效果就是本地完整显示笔记内容～

唯一碰到的问题就是转换不完全。从evernote格式转换到html的时候，总会在图片引用的源代码上留下个&#8221;cid:&#8221;的小尾巴。

先上代码～首先是邮件获取部分  
<!--more-->

  
<code lang='python'>&lt;br />
import imaplib&lt;br />
import email&lt;br />
import StringIO&lt;/p>
&lt;p>gmail_user = 'email'&lt;br />
gmail_pass = 'pass'&lt;br />
M = imaplib.IMAP4_SSL('imap.gmail.com')&lt;br />
M.login(gmail_user, gmail_pass)&lt;/p>
&lt;p>fileHandle = open ( 'mail_all.eml', 'w' )&lt;br />
M.select()&lt;br />
tpe, data = M.search(None, "(UNSEEN)")&lt;br />
if data[0] != '':&lt;br />
    print 'you have new mail'&lt;br />
    for num in data[0].split():&lt;br />
        tpe, data = M.fetch(num, '(RFC822)')&lt;br />
        fileHandle.write ( data[0][1] )&lt;br />
typ, data = M.search(None, 'ALL')&lt;br />
fileHandle.close()&lt;br />
M.close()&lt;br />
M.logout()&lt;br />
</code>  
然后是解码部分  
<code lang='python'>&lt;br />
import email&lt;br />
import re&lt;/p>
&lt;p>fp = open("mail_all.eml", "r")&lt;br />
fileHandle = open("mail_all.html", "w")&lt;br />
msg = email.message_from_file(fp)&lt;br />
subject = msg.get("subject")&lt;br />
h = email.Header.Header(subject)&lt;br />
dh = email.Header.decode_header(h)&lt;br />
subject = dh[0][0]&lt;br />
print "subject:", subject&lt;br />
fileHandle.write ( subject )&lt;br />
print "from: ", email.utils.parseaddr(msg.get("from"))[1]&lt;br />
print "to: ", email.utils.parseaddr(msg.get("to"))[1]&lt;/p>
&lt;p>for par in msg.walk():&lt;br />
	if not par.is_multipart():&lt;br />
		name = par.get_param("name")&lt;br />
		if name:&lt;br />
			h = email.Header.Header(name)&lt;br />
			dh = email.Header.decode_header(h)&lt;br />
			fname = dh[0][0]&lt;br />
			print 'attachment name:', fname&lt;br />
			data = par.get_payload(decode=True)&lt;/p>
&lt;p>			try:&lt;br />
				f = open(fname, 'wb')&lt;br />
			except:&lt;br />
				print 'error, change name'&lt;br />
				f = open('aaaa', 'wb')&lt;br />
			f.write(data)&lt;br />
			f.close()&lt;br />
		else:&lt;br />
			data = par.get_payload(decode=True)&lt;br />
			#get rid of 'cid:' and show pic correctly&lt;br />
			strinfo = re.compile('cid:')&lt;br />
			data = strinfo.sub('',data)&lt;br />
			fileHandle.write ( data )&lt;br />
		print '+'*60&lt;br />
fp.close()&lt;br />
</code>