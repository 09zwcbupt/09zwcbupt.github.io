---
title: 普渡大学Open VSwitch实验视频
author: richard
layout: post
permalink: /2012/08/08/%e6%99%ae%e6%b8%a1%e5%a4%a7%e5%ad%a6open-vswitch%e5%ae%9e%e9%aa%8c%e8%a7%86%e9%a2%91/
categories:
  - 代码
---
分享一段视频，普渡大学关于Open VSwitch的视频。人家其实做的是虚拟化，这个只不过是实验平台而已&#8230;【 P.S. 土豆清晰度不给力&#8230;



附赠实验代码：

./nox_core -i ptcp:6633 vlnswitch&  
ovs-vsctl set-controller br0 tcp:10.0.100.14:6633  
ovs-vsctl set-fail-mode br0 secure

./nox_core -i ptcp:6633 vlnswitch&  
ovs-vsctl set-controller br0 tcp:10.0.100.15:6633  
ovs-vsctl set-fail-mode br0 secure