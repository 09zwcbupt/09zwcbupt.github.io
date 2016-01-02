---
title: Intern @ ARISTA NETWORKS
author: richard
layout: post
permalink: /2014/06/18/intern-life-arista-networks/
dsq_thread_id:
  - 4420748964
categories:
  - Uncategorized
---
<!--:zh-->壹

听之前在这边实习过的学长说，Arista主要用Python和C。后来面试的时候，面试官轻描淡写的说，我们用C++；不会没关系，过来之后学就好了。才问了两个人，口径就不一致了&#8230;

等到入职之后才发现，公司虽说在用，但C++代码只是临时文件一样的地位。程序猿们手写/面对的是更上层的语言（TACC），每次动手也只需要修改Entity之间的逻辑关系。每当编译的时候，TACC代码就会通过编译器生成C++中对应的各种类以及类中的接口函数。这么做一个明显的好处是，搭建系统的时候速度会非常快。举个例子，入职培训中有一个简单的教程，是关于怎么写一个系统插件。按照这个教程写下来，TACC代码大概是50行，但是编译到C++后，代码变到了2000行以上&#8230;

关于TACC，有一个介绍文档：



<div style="margin-bottom: 5px;">
  <strong> <a title="SDEC2011 Going by TACC" href="https://www.slideshare.net/sdec2011/sdec2011-going-by-tacc" target="_blank">SDEC2011 Going by TACC</a> </strong> from <strong><a href="http://www.slideshare.net/sdec2011" target="_blank">Korea Sdec</a></strong>
</div>

<div style="margin-bottom: 5px;">
</div>

顺便八一卦，这个TACC是另一个公司(OptumSoft)的产品。这个公司是和Arista一起成长起来的，不仅员工在两个公司创立之初时一起工作，就连OptumSoft的创始人David Cheriton也是Arista的创始人之一。此外，Arista还是TACC唯一的用户。这些看起来都很美好，然后事情就变得狗血起来&#8230; Arista的发展非常成功，公司规模逐渐扩大，也搬进了现在所在的大楼，外加准备上市；但是OptumSoft却没那么顺利，被认为会是一个失败的创业项目。不知道David Cheriton是中了什么邪，就在Arista准备上市+自己将会是最大的持股人的时候讲其告上法庭，并且企图获得TACC的改进，乃至通过TACC生成的软件（包括Arista Switch的操作系统）的所有权。业内人士纷纷表示呵呵，很多人都认为这种奇葩的做法只是为了挽救OptumSoft。好在Arista在我入职后的第一个周五成功上市。

贰 &#8211; BPF

第一个项目很简单，作为练手+熟悉系统。第二个就复杂些。其中一个环节是加入BPF。没什么好写的，直接上参考链接:

<div style="margin-bottom: 5px;">
  <ol>
    <li>
      McCanne, Steven; Jacobson, Van (1992-12-19). &#8220;<a title="McCanne, Steven; Jacobson, Van (1992-12-19). " href="http://www.tcpdump.org/papers/bpf-usenix93.pdf" target="_blank">The BSD Packet Filter: A New Architecture for User-level Packet Capture</a>&#8220;
    </li>
    <li>
      <a title="Berkeley Packet Filters – The Basics Jeff Stebelton" href="http://www.infosecwriters.com/text_resources/pdf/JStebelton_BPF.pdf" target="_blank">Berkeley Packet Filters – The BasicsJeff Stebelton</a>
    </li>
    <li>
      [kernel doc]<a title="Linux Socket Filtering aka Berkeley Packet Filter (BPF)" href="https://www.kernel.org/doc/Documentation/networking/filter.txt" target="_blank">Linux Socket Filtering aka Berkeley Packet Filter (BPF)</a>
    </li>
    <li>
      [FreeBSD man 4]<a title="Berkeley Packet Filter" href="http://www.freebsd.org/cgi/man.cgi?query=bpf&sektion=4&apropos=0&manpath=FreeBSD+10.0-RELEASE" target="_blank">Berkeley Packet Filter</a>
    </li>
    <li>
      [FreeBSD man 9]<a title="Berkeley Packet Filter" href="http://www.freebsd.org/cgi/man.cgi?query=bpf&sektion=9&apropos=0&manpath=FreeBSD+10.0-RELEASE" target="_blank">Berkeley Packet Filter</a>
    </li>
    <li>
      <a title="Programming with pcap" href="http://www.tcpdump.org/pcap.html" target="_blank">Programming with pcap</a>
    </li>
  </ol>
</div>

ENG:

<!--:-->

<!--:en-->1



<div style="margin-bottom: 5px;">
  <strong> <a title="SDEC2011 Going by TACC" href="https://www.slideshare.net/sdec2011/sdec2011-going-by-tacc" target="_blank">SDEC2011 Going by TACC</a> </strong> from <strong><a href="http://www.slideshare.net/sdec2011" target="_blank">Korea Sdec</a></strong>
</div>

&nbsp;

2

As part of project 2 is related to BPF, I am learning BPF and searching for tutorials. The kernel document seems to be good learning material, however the example program is not runnable. So, I wrote a <a title="socket filter" href="https://github.com/09zwcbupt/personal/blob/master/bpf/sock_filter.c" target="_blank">version</a> based on it (using socket filter in linux), and also <a title="pcap bpf" href="https://github.com/09zwcbupt/personal/blob/master/bpf/pcap_bpf.c" target="_blank">another version</a> using functions in libpcap to generate rules and filter packets.

Basically, BPF is used on raw sockets to filter out traffic that is not interesting. But it turns out that the filter also works with datagram socket (UDP socket). According to <a title="Using BPF with SOCK_DGRAM on Linux machine" href="http://stackoverflow.com/questions/24514333/using-bpf-with-sock-dgram-on-linux-machine" target="_blank">Using BPF with SOCK_DGRAM on Linux machine</a>, as the compiled filter works on bytes that is received from sockets, plus the UDP socket can see from the UDP layer of the packet, the meaning of \`ldb 0\` is changed from reading the first byte of destination MAC address to reading the first byte of the source port. This change means I&#8217;ll have trouble if I am using libpcap generated filter code on a UDP socket. And to solve that, either change the rule in to some meaning less combination (like &#8220;udp[8] == 0x00&#8243; -> &#8220;ether[8] == 0x00&#8243;), or try to adjust generated code to load proper byte of the received packet.

Reference:

  1. McCanne, Steven; Jacobson, Van (1992-12-19). &#8220;<a title="McCanne, Steven; Jacobson, Van (1992-12-19). " href="http://www.tcpdump.org/papers/bpf-usenix93.pdf" target="_blank">The BSD Packet Filter: A New Architecture for User-level Packet Capture</a>&#8220;
  2. <a title="Berkeley Packet Filters – The Basics Jeff Stebelton" href="http://www.infosecwriters.com/text_resources/pdf/JStebelton_BPF.pdf" target="_blank">Berkeley Packet Filters – The BasicsJeff Stebelton</a>
  3. [kernel doc]<a title="Linux Socket Filtering aka Berkeley Packet Filter (BPF)" href="https://www.kernel.org/doc/Documentation/networking/filter.txt" target="_blank">Linux Socket Filtering aka Berkeley Packet Filter (BPF)</a>
  4. [FreeBSD man 4]<a title="Berkeley Packet Filter" href="http://www.freebsd.org/cgi/man.cgi?query=bpf&sektion=4&apropos=0&manpath=FreeBSD+10.0-RELEASE" target="_blank">Berkeley Packet Filter</a>
  5. [FreeBSD man 9]<a title="Berkeley Packet Filter" href="http://www.freebsd.org/cgi/man.cgi?query=bpf&sektion=9&apropos=0&manpath=FreeBSD+10.0-RELEASE" target="_blank">Berkeley Packet Filter</a>
  6. <a title="Programming with pcap" href="http://www.tcpdump.org/pcap.html" target="_blank">Programming with pcap</a>

<!--:-->