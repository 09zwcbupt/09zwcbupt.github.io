---
title: '[chrome插件]API文档：TAG'
author: richard
layout: post
permalink: /2012/09/24/chrome%e6%8f%92%e4%bb%b6api%e6%96%87%e6%a1%a3%ef%bc%9atag/
categories:
  - 代码
---
谷歌给的API虽然清晰，但是在具体用法上面做的有点过于精简。所以，有必要先花点时间把浏览器的API特性摸清楚，然后动手实践消化。

## API Reference: chrome.tabs

<div>
  <h3 id="types">
    Types
  </h3>
  
  <h3>
    Tab
  </h3>
  
  <div style="text-align: left;">
    ( object ) 
    
    <dl>
      <dt>
        status ( optional string )
      </dt>
      
      <dd>
        Either <em>loading</em> or <em>complete</em>. 两个状态2选1
      </dd>
      
      <dt>
        index ( integer )
      </dt>
      
      <dd>
        The <span style="color: #ff0000;">zero-based</span> index of the tab within its window.初始为0的ID，从左向右依次加1，页面交换顺序ID依照顺序变化。
      </dd>
      
      <dt>
        openerTabId ( optional integer )
      </dt>
      
      <dd>
        The ID of the tab that opened this tab, if any. This will only be present if the opener tab still exists.写的够清楚了&#8230;
      </dd>
    </dl>
    
    <dl>
      <dt>
        title ( optional string )
      </dt>
      
      <dd>
        The title of the tab. This may not be available if the tab is loading. 另外，如果title是动态的话，这个属性只保存着切换到tab时的title。如果之后title有变化，这个属性中不会有体现。<!--more-->
      </dd>
      
      <dt>
        url ( string )
      </dt>
      
      <dd>
        The URL the tab is displaying.
      </dd>
      
      <dt>
        pinned ( boolean )
      </dt>
      
      <dd>
        Whether the tab is pinned.
      </dd>
      
      <dt>
        highlighted ( boolean )
      </dt>
      
      <dd>
        Whether the tab is highlighted.
      </dd>
      
      <dt>
        windowId ( integer )
      </dt>
      
      <dd>
        The ID of the window the tab is contained within.
      </dd>
      
      <dt>
        active ( boolean )
      </dt>
      
      <dd>
        Whether the tab is active in its window.
      </dd>
      
      <dt>
        favIconUrl ( optional string )
      </dt>
      
      <dd>
        The URL of the tab&#8217;s favicon. This may not be available if the tab is loading.
      </dd>
      
      <dt>
        id ( integer )
      </dt>
      
      <dd>
        The ID of the tab. Tab IDs are unique within a browser session. ID的编号规则实在是很有意思&#8230;
      </dd>
      
      <dt>
        incognito ( boolean )
      </dt>
      
      <dd>
        Whether the tab is in an incognito window.
      </dd>
    </dl>
  </div>
</div>

函数方面，chrome.tabs.executeScript(integer tabId, object details, function callback)这个函数还是非常有用，是Programmatic injection很好的一种实现方式。参数中，第一个参数是内容脚本所在的tab id，第二参数是脚本内容（可以选择code+脚本、file+.js文件等方式）。第三为可选响应回调函数参数。

另外，get类函数都有这样一个特点（或者说，tabs、windows中类似的函数有这样一个特点），就是参数是一个回调函数。并且，函数在回调函数中将传递一个tabs、windows对象，通过该对象可以获取窗口的基本信息。省下很多函数暂时用不到，先不写太多~lol

官方文档地址：<http://developer.chrome.com/extensions/tabs.html>