---
title: '[转载]The Northbound API is the key to OpenFlow’s Success'
author: richard
layout: post
permalink: /2012/11/13/%e8%bd%ac%e8%bd%bdthe-northbound-api-is-the-key-to-openflows-success/
categories:
  - 技术
tags:
  - API
  - System
---
最近申请忙的要死，也没有多少时间没发文章&#8230;

今天转载一份，[SDN Central][1]11月8号的文章：The Northbound API is the key to OpenFlow’s Success。文章主要讨论了API对于SDN/OpenFlow的重要意义，下面是正文

* * *

![Puzzle Piece][2]

The Southbound interface between the <a title="SDNCentral Shipping Products" href="http://www.sdncentral.com/shipping-sdn-products/" target="_blank">switch</a> and the<a title="SDNCentral Announced SDN Products" href="http://www.sdncentral.com/announced-sdn-products/" target="_blank"> controller</a> was key to significant [SDN][3]possibilities.  However, the Northbound interface between orchestration and management systems with the controller will determine the success OpenFlow achieves in the network.

[It][4] is important to recognize that the OpenFlow controller is not necessarily a management platform.  It provides a standard and controlled interface to the data plane.  Without it, the idea of SDN requires communication directly to a network device.  The leading network vendors are currently promoting this approach when they talk about their SDN solutions.  While that meets the definition of “Software Defined Networking”, it is a short-sighted vision of the future network.  It would require every agent that wished to interact with the network to know about every device in the network (or at least those it wishes to control – and how does it know that?).<!--more-->

A controller, that has visibility into the entire network is the central control point.  But, the controller should not become a monolithic everything application.  Instead, it should interface with separate systems providing both updates about network performance and an interface for systems to provide network and security orchestration. These orchestration and management applications are the true brain of an OpenFlow network.  The controller is a middle-man.  And this is why the <a title="OpenFlow Northbound API – A New Olympic Sport" href="http://www.sdncentral.com/sdn-blog/openflow-northbound-api-olympics/2012/07/" target="_blank">Northbound API</a> is so critical.

This Northbound API is not defined today.  The <a title="ONF" href="http://www.sdncentral.com/listings/open-networking-foundation" target="_blank">ONF</a> has taking the initial steps of <a href="https://www.opennetworking.org/new-working-groups/" rel="nofollow" target="_blank">creating a discussion group</a>.  While this is short of a full working group to define an <a title="SDN Resources: API" href="http://www.sdncentral.com/comprehensive-list-of-sdn-apis/" target="_blank">API</a>, it is a pragmatic step that is likely to result in active projects such as <a href="http://www.sdncentral.com/comprehensive-list-of-open-source-sdn-projects/" target="_blank">OpenStack</a> that are moving rapidly to influence the resulting API.  This is likely going to result in the continuation of proprietary API’s for sometime to come, but also result in rapid expansion of the Northbound API.  It may be chaotic, but I think this has the potential of creating a robust API in a short amount of time, which will be critical to the success of OpenFlow.

The possibilities of SDN, in particular OpenFlow, are exciting.  But to see the possible become reality will depend on how quickly a capable and usable Northbound API is developed.

**Guest Blogger Disclaimer:**

*The views, opinions and positions expressed within these guest posts are those of the author alone and do not represent those of *<a href="http://sdncentral.com/" rel="nofollow" target="_blank"><em>SDNCentral.com</em></a>* and SDNCentral, LLC. The accuracy, completeness and validity of any statements made within this article are not guaranteed. We accept no liability for any errors, omissions or representations. The copyright of this content belongs to the author and any liability with regards to infringement of intellectual property rights remains with them.*

 [1]: http://www.sdncentral.com
 [2]: http://www.sdncentral.com/wp-content/uploads/2012/11/Puzzle-Piece.jpg "Puzzle Piece"
 [3]: http://www.sdncentral.com/products-technologies/hp-throws-down-the-gauntlet-in-the-sdn-arena/2012/10/
 [4]: http://www.sdncentral.com/guest-blog-posts/how-network-virtualization-has-helped-shaped-ha-and-disaster-recovery/2012/11/