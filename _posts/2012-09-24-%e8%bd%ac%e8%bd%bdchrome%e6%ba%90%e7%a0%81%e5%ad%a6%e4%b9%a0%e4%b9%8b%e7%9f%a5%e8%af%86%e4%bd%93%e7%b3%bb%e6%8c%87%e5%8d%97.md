---
title: '[转载]chrome源码学习之知识体系指南'
author: richard
layout: post
permalink: /2012/09/24/%e8%bd%ac%e8%bd%bdchrome%e6%ba%90%e7%a0%81%e5%ad%a6%e4%b9%a0%e4%b9%8b%e7%9f%a5%e8%af%86%e4%bd%93%e7%b3%bb%e6%8c%87%e5%8d%97/
categories:
  - 代码
---
其实只是做点chrome插件开发，对于这个浏览器的架构并不打算深入去纠结什么。不过看到这篇文章写得很不错，还是转来收藏着~lol

原文地址：[chrome源码学习之知识体系指南][1]

* * *

<span style="font-size: medium;">google chrome浏览器的源代码是非常庞大的，为了较快的进入学习状态，有必要事先对一些知识点进行说明，这里不是要详细说明里面的细节，而是从概念层次阐明一些注意事项。这里谈到的东西也不一定说非要事先把这些东西搞得很明白才能去学习源代码，主要还是先给大家一个心理准备。当然如果你最终要在细粒度的层次掌握源代码细节，那么这些知识点必须非常清楚，不过这可以结合源代码的时候再针对性的来澄清这些知识点。</span>

<span style="font-size: medium;">由于chrome源代码包含方方面面的技术非常之多，根据个人喜好可能针对性的对某些技术感兴趣，那么可以针对性的进行学习。大的原则是理论和实践相结合，chrome包含的代码就是各种规范、理论的具体实践实现。</span>

## <a name="t0"></a>基础知识<!--more-->

<span style="font-size: medium;">基础知识是任何技术方面都应该掌握的领域无关的通用知识。我认为主要包括“语言基础”和“系统基础”两大类。</span>

## <a name="t1"></a><span style="color: #000000;"><strong>语言基础知识</strong></span>

<span style="font-size: medium;">整个chrome源代码包括webkit内核、v8引擎全部用c++语言编写。那么作为语言基础的c++语言就必须是精通的水平才可能流畅的看明白里面的代码。我一直认为c++是有史以来最复杂的语言（可参考孟岩文章<a href="http://blog.csdn.net/myan/archive/2004/10/23/148900.aspx" target="_blank">关于C++复杂性的零碎思考</a>），是典型的魔幻语言，我曾经也痴迷去深究c++一些高级技巧，后来某天突然发现这种深究、这种玩法除了增加理解上的复杂性，对实际问题似乎并没有带来任何好处。后来看到一篇文章（请看孟岩文章<a href="http://blog.csdn.net/myan/archive/2008/01/07/2028545.aspx" target="_blank">Ruby 1.9不会杀死Python</a>），才明白原来自己的性格是喜欢简约风格的语言，从此不再去钻牛角尖玩语言技巧。对于语言问题每个人都有自己的看法和偏好，但显然，不喜欢归不喜欢，但在现实中，我们有时候又必须去面对我们不太喜欢的东西(当然并不是说我讨厌c++)，拿语言来说，这种情况下对于喜欢简约风格的程序员最理智的办法就是以一种简约的方法去使用复杂的c++。千万不要在实际应用中为了技巧而技巧，这样会非常丑陋别扭，因为你根本没有真正明白什么时候该合理的使用这些技巧。好在chrome源代码里面的c++语言技巧绝不是为了故弄玄虚，在chrome里面作者们为我们展示了如何恰到好处的使用这些技巧来解决实际问题，如果你曾经困惑过c++里面一些技巧究竟有何实际用途，或者对这些技巧理解不深，那么在chrome里可以找到很好的答案。扯得有点远了，现在还是总结一下chrome里面关于c++语言层面的一些知识点。</span>

> <span style="font-size: medium;"><strong>STL</strong>：标准库的使用，这个很基本，没有什么好说的。</span>
> 
> <span style="font-size: medium;"><strong>C++对象生命周期管理技术</strong>：这可以说是c++应用开发中永远的痛，很多的内存访问错误与此有关。对于简单的过程化应用，我们可以很简单的遵循谁分配对象谁就负责释放对象的原则。但在大型应用中，对象生命周期的管理变得非常的复杂，不可能简单的遵循谁分配谁释放原则，这在chrome这样的大型项目中表现极其突出。在chrome中，对象的出生、生活、死亡经常在不同的上下文线程中完成。在chrome中主要采用了基于引用计数原理来管理对象生命周期，同时有针对不同场合的变体。另外还有类似智能指针这样的方案。如果你要将对chrome代码做改造为我所用，对象的生死问题必须小心对待。</span>
> 
> <span style="font-size: medium;"><strong>模板特化（Template Specialization）</strong>：c++里面所谓的一些高级特性总是离不开模板的，也正是模板的引入让c++变得非常复杂。模板特化在chrome的ipc通信体系中，对参数进行序列化的时候用到了这个特性。</span>
> 
> <span style="font-size: medium;"><strong>C++ 元组（Tuple）实现技术</strong>：也是通过模板技术来实现。</span>
> 
> <span style="font-size: medium;"><strong>类型萃取技术(Traits)：</strong>c++泛型编程的重要技术之一。</span>
> 
> <span style="font-size: medium;"><strong>宏技巧</strong>：在消息映射实现部分，用到了一个很有意思的手法，定义一次宏，展开多段代码，同时完成了消息ID枚举值定义和消息类的定义。</span>
> 
> <span style="font-size: medium;"><strong>类成员函数指针</strong>：相对于模板，这个容易理解多了。</span>

<span style="font-size: medium;">以上关于STL、模板相关的一些知识可以参考《STL源码剖析》和《C++设计新思维》，我认为把这两本书看明白了，C++水平可以配称“精通”了。另外我可以负责的说，把chrome里面涉及到的c++语言层面的东西都能彻底明白，那么c++水平也足够用了。</span>

## <a name="t2"></a><span style="color: #000000;"><strong>系统基础知识</strong></span>

<span style="font-size: medium;">这里主要指的是操作系统基础知识，chrome浏览器作为跨平台浏览器，在linux、windows、mac os上均有对应的实现版本。对于很多标准性的、通用性的操作系统特性，chrome提供了抽象接口，具体在不同的操作系统上对应有不同的实现。我这里以windows为例，值得关注的知识点包括：</span>

> <span style="font-size: medium;"><strong>进程、线程概念</strong>：chrome是多进程体系结构，多线程就不用说了，必定是多线程。那么要深刻理解这样的体系结构，就需要对操作系统进程、线程概念非常清楚。</span>
> 
> <span style="font-size: medium;"><strong>线程同步</strong>：多线程如何同步的问题。</span>
> 
> <span style="font-size: medium;"><strong>线程本地存储（TLS）</strong>：利用TLS存储线程私有数据。</span>
> 
> <span style="font-size: medium;"><strong>Windows内核对象</strong>：包括事件对象、互斥体等内核对象用于线程同步。</span>
> 
> <span style="font-size: medium;"><strong>进程IPC</strong>：多进程结构就必定涉及到进程如何通信的问题，这就是操作系统提供的IPC机制。在chrome的windows版本中采用的是“命名管道”来作为IPC通信基础。</span>
> 
> <span style="font-size: medium;"><strong>共享内存</strong>：为了减少进程之间的大数据传递，采用共享内存技术来减少数据搬动开销。</span>
> 
> <span style="font-size: medium;"><strong>完成端口</strong>：Windows操作系统高效的异步IO模型，chrome中线程消息循环使用了完成端口。</span>
> 
> <span style="font-size: medium;"><strong>Socket IO 模型</strong>：http客户端协议实现采用的socket io模型包括重叠io和事件选择。</span>
> 
> <span style="font-size: medium;"><strong>定时器</strong>：很多任务采用操作系统提供的定时器API来完成。</span>
> 
> <span style="font-size: medium;"><strong>操作系统异常机制</strong>：对异常的挂接处理，需利用操作系统提供的相关api来进行。</span>
> 
> <span style="font-size: medium;"><strong>UI交互机制</strong>：chrome最终是要展示很多native UI的，在windows中，chrome采用skia图形库结合操作系统消息机制自己封装了一套界面元素。</span>

<span style="font-size: medium;">关于操作系统相关的基础知识，可以参考《Windows核心编程》和《Win32 多线程程序设计》。</span>

## <a name="t3"></a>设计模式知识

> <span style="font-size: medium;">设计模式是编写高质量、高扩展性代码的基础，chrome代码中主要用到了下列一些设计模式：</span>
> 
> <span style="font-size: medium;"><strong>工厂模式</strong></span>
> 
> <span style="font-size: medium;"><strong>观察者模式</strong></span>
> 
> <span style="font-size: medium;"><strong>单件模式</strong></span>
> 
> <span style="font-size: medium;"><strong>命令模式</strong></span>
> 
> <span style="font-size: medium;"><strong>代理模式</strong></span>
> 
> <span style="font-size: medium;"><strong>适配器模式</strong></span>
> 
> <span style="font-size: medium;"><strong>委托模式</strong></span>
> 
> <span style="font-size: medium;">关于设计模式方面的书籍，首推当然是“四人帮”的《设计模式－可复用面向对象软件的基础》，此书非常的精练，内容就难免有些抽象。所以并不适合初学者，要通俗生动一点的可以参考《head first 设计模式》，该书也非常不错。</span>

## <a name="t4"></a>领域知识

> <span style="font-size: medium;">作为web浏览器，其领域知识当然是w3c标准了。要深刻理解webkit的实现，必然要对相关规范有所了解。</span>
> 
> <span style="font-size: medium;"><strong>HTML4/HTML5规范</strong></span>
> 
> <span style="font-size: medium;"><strong>CSS2/CSS3规范</strong></span>
> 
> <span style="font-size: medium;"><strong>DOM2/DOM3规范</strong></span>
> 
> <span style="font-size: medium;"><strong>JavaScript语言规范</strong></span>
> 
> <span style="font-size: medium;"><strong>HTTP协议规范</strong></span>
> 
> <span style="font-size: medium;">以上是整个web浏览器所涉及到的最核心的几个方面的规范标准，当然里面还有更多的外围相关标准。这些规范直接阅读w3c标准是比较抽象枯燥的，好在这些领域知识所涉及到的相关技术资料已经非常丰富了。可以从web前端应用开发层着手，结合webkit代码、规范文件来理解这些规范。</span>
> 
> <span style="font-size: medium;">除了上述webcore相关领域知识外，还有一些基础设施领域，包括：</span>
> 
> <span style="font-size: medium;"><strong>图形领域知识</strong>：chrome采用的是skia图形引擎作的页面渲染，如果对skia比较有兴趣，这是很好的学习材料，但前提最好是有图形学基础理论知识。</span>
> 
> <span style="font-size: medium;"><strong>数据库领域</strong>：chrome对cookie的管理，采用的是sqlite开源数据库，如果对数据库技术感兴趣，可以学习。</span>
> 
> <span style="font-size: medium;"><strong>数据压缩技术</strong>：zlib这样的基础库。</span>
> 
> <span style="font-size: medium;"><strong>图片解码</strong>：jpeg、png等图片格式解码。</span>
> 
> <span style="font-size: medium;"><strong>XML解析</strong>：expat</span>
> 
> <span style="font-size: medium;"><strong>分布式数据序列化</strong>：protobuf2库，该库是google比较核心的一个基础技术，它是基于二进制的。很好的平衡了对象化和效率之间的取舍。</span>
> 
> <span style="font-size: medium;"><strong>多媒体技术</strong>：网页上的音频视频处理。</span>
> 
> <span style="font-size: medium;"><strong>安全技术</strong>：SSL，加密解密、数字签名。这些都可以在里面找到相关的学习材料。</span>
> 
> <span style="font-size: medium;"><strong>UI框架</strong>：chrome的ui元素是采用了单独的一个view库来封装不同操作系统下的ui机制，如果对ui交互框架感兴趣，可以重点关注view库的实现代码。</span>
> 
> <span style="font-size: medium;"><strong>字符串处理（UNICODE）/国际化</strong>：这部分的技术主要是利用非常强大的icu库来支撑的。</span>
> 
> <span style="font-size: medium;"><strong>CRT运行库的内存管理技术：</strong>采用了tcmalloc库来替换系统提供的内存管理crt库，大大提供内存管理的效率和速度。</span>
> 
> <span style="font-size: medium;">对于上述工具性基础设施，我想作为应用整合者，更多的可能是从各个库的API层面入手，先在使用层面达到很熟练的程度，这样可以方便的为自己的实际项目服务。至于内部实现细节我想有兴趣去深究的人不会很多。</span>
> 
> &nbsp;

## <a name="t5"></a>总结

<span style="font-size: medium;">上面只是一个对chrome源代码知识内容很初步很粗的简单的罗列，目的是从概念层次上先有个简单的了解。具体细节里面当然是非常之多。具体情况请根据自身的需要结合源代码选择性、针对性的进行学习。至于我的重点可能包括chrome体系结构、webkit内核、工具库中的protobuf2这几部分内容。</span>

 [1]: http://blog.csdn.net/ciml/article/details/5721153