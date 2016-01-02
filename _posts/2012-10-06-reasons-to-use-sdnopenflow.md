---
title: Why SDN/OpenFlow
author: richard
layout: post
permalink: /2012/10/06/reasons-to-use-sdnopenflow/
categories:
  - 技术
---
As we know, Google and Yahoo! have implement SDN architecture into part of their Data Centers as an experiment. But what have the two companies thought about? And how did they find SDN useful? Here I select lines from their ppts, and these lines are exactly the reasons why G&Y did so.

<span style="font-size: x-large;"><strong>Reasons from Google:</strong></span>

### <span style="text-decoration: underline;">Subhasree Mandal October 17, 2011</span><sup>[1]</sup>

<div>
       1、Utilize more powerful compute resources
</div>

<div>
       2、Supports easier upgrade, experimental features
</div>

<div>
       3、Target loop-free, sequenced, centralized routing
</div>

<div>
       4、Enables advanced features like centralized TE
</div>

### <span style="text-decoration: underline;">On 2012 ONS meeting</span><sup>[2]</sup>

#### 

####      **CAPEX:**

<div>
            make efficient use of resources
</div>

<div>
                 ● network element cpu and memories
</div>

<div>
                 ● underlying network capacity
</div>

<div>
            move heaviest workloads off of expensive, relatively slow embedded systems to cheap, fast, commodity hardware
</div>

<div>
            provide visibility into and synchronized control of network state such that underlying capacity may be used more efficiently
</div>

#### <!--more-->

####      **OPEX:**

<div>
            Reduce network complexity and thus operational overhead and outage time
</div>

<div>
            simplify policy composition
</div>

<div>
            enforce correctness constraints and invariants
</div>

<div>
            <strong>reduce inter-dependendencies</strong>
</div>

<div>
                 ○ between protocols
</div>

<div>
                 ○ between routers
</div>

<div>
            reduce complexity of distributed control system software
</div>

<div>
            implement potentially innovative new techniques (eg: Heller et al&#8217;s Elastic Trees)
</div>

<div>
</div>

<div>
</div>

<span style="font-size: x-large;"><strong>Reasons from Yahoo：</strong></span>

### <span style="text-decoration: underline;">2012 ONS meeting</span><sup>[3]</sup>

<div>
  <div>
    <div>
           <strong>Topology Discovery</strong>
    </div>
    
    <div>
                • Today:
    </div>
    
    <div>
                     Routers spend 30%+ cpu cycles re-doing that topology discovery
    </div>
    
    <div>
                          – Edge discovery
    </div>
    
    <div>
                          – ARP/MAC bindings
    </div>
    
    <div>
                          – Topology discovery
    </div>
    
    <div>
                          – ISIS/OSPF/SPT/RSTP/TRILL/etc
    </div>
    
    <div>
                • SDN:
    </div>
    
    <div>
                     We already have this info in a central DB!
    </div>
    
    <div>
                     So, let’s just program it!
    </div>
    
    <div>
    </div>
    
    <div>
           <strong>Cost</strong>
    </div>
    
    <div>
                It’s all about the <span style="color: #ff0000;"><strong>$$$$$</strong></span>
    </div>
    
    <div>
    </div>
    
    <div>
           <strong>Automation</strong>
    </div>
    
    <div>
                • Today:
    </div>
    
    <div>
                     Powerful configuration templating tools
    </div>
    
    <div>
                          • Create config generators to translate those templates to every vendor/device/OS model syntax
    </div>
    
    <div>
                     Configuration deployment tools to push that out
    </div>
    
    <div>
                          • They are absolutely archaic
    </div>
    
    <div>
                          • Don’t you just love expect?
    </div>
    
    <div>
                • SDN:
    </div>
    
    <div>
                     General API
    </div>
    
    <div>
                     Easier to get stuff done..
    </div>
    
    <div>
    </div>
    
    <div>
          <strong> Faster Innovation</strong>
    </div>
    
    <div>
                • Today:
    </div>
    
    <div>
                     Customer: “I need a new feature X please”
    </div>
    
    <div>
                     Vendor: “ But you are the <strong>only one </strong>asking for that, so, how much revenue will that bring in?”
    </div>
    
    <div>
                     =><strong>conflict</strong>
    </div>
    
    <div>
                • SDN:
    </div>
    
    <div>
                     Allows for network “plug-ins” into the controller
    </div>
    
    <div>
                     Now you can develop your own control features
    </div>
    
    <div>
    </div>
    
    <div>
    </div>
    
    <div>
      [1]. <a title="[1]" href="http://www.tektalk.org/wp-content/uploads/2012/04/OpenFlowTutorial-Google.pdf" target="_blank">http://www.tektalk.org/wp-content/uploads/2012/04/OpenFlowTutorial-Google.pdf</a>
    </div>
    
    <div>
      [2]. <a title="[2]" href="http://static.techfieldday.com/wp-content/uploads/2011/10/TheLongRoadtoSDN.pdf" target="_blank">http://static.techfieldday.com/wp-content/uploads/2011/10/TheLongRoadtoSDN.pdf</a>
    </div>
    
    <div>
      [3]. <a title="[3]" href="http://static.techfieldday.com/wp-content/uploads/2011/10/Y_warehouse-SDN-v2.pdf" target="_blank">http://static.techfieldday.com/wp-content/uploads/2011/10/Y_warehouse-SDN-v2.pdf</a>
    </div>
  </div>
</div>