---
title: Packet_In事件架构
author: richard
layout: post
permalink: /2012/08/06/packet_in%e4%ba%8b%e4%bb%b6%e6%9e%b6%e6%9e%84/
categories:
  - 代码
---
[<img class="size-full wp-image-171 alignnone" title="PacketIn事件" src="http://richardzhao.me/wp-content/uploads/2012/08/PacketIn事件.png" alt="" width="1294" height="521" />][1]

event中packet类型判断方式  
1、if isinstance(event.parsed.next, arp): [利用函数判断]  
2、if packet.type == ethernet.LLDP_TYPE: [利用ethernet中定义的类型判断]

<!--more-->用debug信息打印packet信息的语句

  
添加在l3_learning.py的91行  
<code lang="python">&lt;br />
def _handle_PacketIn (self, event): #[line90]&lt;br />
log.debug("") #[line91]&lt;br />
log.debug(" PacketIn Information ")&lt;br />
log.debug("--------------------------------------------")&lt;br />
log.debug("dpid: %d",event.connection.dpid)&lt;br />
log.debug("packet_type: %x",event.parsed.type)&lt;br />
log.debug("ethernet_src:%s",str(event.parsed.src))&lt;br />
log.debug("ethernet_dst:%s",str(event.parsed.dst))&lt;br />
if isinstance(event.parsed.next, ipv4):&lt;br />
log.debug("packet_type: IP")&lt;br />
log.debug("IP_VERSION: %u",event.parsed.next.v)&lt;br />
log.debug("packet_type: %u",event.parsed.next.ttl)&lt;br />
log.debug("packet_id: %u",event.parsed.next.id)&lt;br />
log.debug("packet_csum: %u",event.parsed.next.csum)&lt;br />
log.debug("packet_ip_id:%u",event.parsed.next.ip_id)</code>

if isinstance(event.parsed.next, arp):  
log.debug(&#8220;packet_type: ARP&#8221;)  
log.debug(&#8220;src_ip: %s&#8221;,str(event.parsed.next.protosrc))  
log.debug(&#8220;dst_ip: %s&#8221;,str(event.parsed.next.protodst))  
log.debug(&#8220;src_mac: %s&#8221;,str(event.parsed.next.hwsrc))  
log.debug(&#8220;dst_mac: %s&#8221;,str(event.parsed.next.hwdst))

log.debug(&#8220;buffer\_id: %d&#8221;,event.ofp.buffer\_id)  
log.debug(&#8220;event-type: %s&#8221;,str(event.\_\_class\_\_))  
log.debug(&#8220;port: %d&#8221;,event.port)  
log.debug(&#8220;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8211;&#8220;)  
log.debug(&#8220;&#8221;)

 [1]: http://richardzhao.me/wp-content/uploads/2012/08/PacketIn事件.png