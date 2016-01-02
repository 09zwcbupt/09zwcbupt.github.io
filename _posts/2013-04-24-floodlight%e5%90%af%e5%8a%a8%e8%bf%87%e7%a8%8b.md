---
title: FloodLight模块加载过程
author: richard
layout: post
permalink: /2013/04/24/floodlight%e5%90%af%e5%8a%a8%e8%bf%87%e7%a8%8b/
dsq_thread_id:
  - 4426735548
categories:
  - 代码
---
模块加载部分：

> core/module/FloodlightModuleLoader.java  =>  (396 &#8211; 403) 

loadModulesFromList函数  
<code lang="java" width="600">&lt;br />
for (IFloodlightModule module : moduleSet) {&lt;br />
    // init the module&lt;br />
    if (logger.isDebugEnabled()) {&lt;br />
        logger.debug("Initializing " +  module.getClass().getCanonicalName());&lt;br />
    }&lt;br />
    module.init(floodlightModuleContext);&lt;br />
}&lt;br />
</code>  
循环加载启动列表中的模块。其中module.init(floodlightModuleContext);执行  
<!--more-->

> core/module/IFloodlightModule.java => (77 &#8211; 88) 

Interface，转换到模块override的init函数。  
<code lang="java" width="600">&lt;br />
void init(FloodlightModuleContext context) throws FloodlightModuleException;&lt;/p>
&lt;p>/**&lt;br />
 * This is a hook for each module to do its &lt;em>external&lt;/em> initializations,&lt;br />
 * e.g., register for callbacks or query for state in other modules&lt;br />
 *&lt;br />
 * It is expected that this function will not block and that modules that want&lt;br />
 * non-event driven CPU will spawn their own threads.&lt;br />
 *&lt;br />
 * @param context&lt;br />
 * @throws FloodlightModuleException&lt;br />
 */&lt;br />
</code>

随后执行初始化完成的组件中的startUp函数。对于如下的事件绑定代码  
<code lang="java" width="600">&lt;br />
floodlightProvider.addOFMessageListener(OFType.PACKET_IN, this);&lt;br />
</code>

> core/internal/Controller.java ==> (1451 &#8211; 1460)

<code lang="java" width="600">&lt;br />
//line 149 声明messageListeners实例&lt;br />
protected ConcurrentMap&lt;oftype,
                        ListenerDispatcher&lt;oftype,IOFMessageListener>>&lt;br />
                            messageListeners;&lt;br />
//line 1446&lt;br />
// ***************&lt;br />
// IFloodlightProvider&lt;br />
// ***************&lt;/p>
&lt;p>@Override&lt;br />
public synchronized void addOFMessageListener(OFType type,&lt;br />
                                              IOFMessageListener listener) {&lt;br />
    ListenerDispatcher&lt;oftype, IOFMessageListener> ldd =&lt;br />
        messageListeners.get(type); //从messageListeners中获取tpye事件的监听列表&lt;br />
    if (ldd == null) {     //先检测对应事件列表ldd是否为空&lt;br />
        ldd = new ListenerDispatcher&lt;oftype, IOFMessageListener>();&lt;br />
        messageListeners.put(type, ldd);&lt;br />
    }&lt;br />
    ldd.addListener(type, listener);&lt;br />
}&lt;br />
</code>  
其中，ldd是事件注册列表（具体属性：listeners ArrayList<e> (id=187)）。ListenerDispatcher类的具体定义位置是core/util/ListenerDispatcher.java。Debug中，PacketIn事件的监听模块默认为：

`<br />
elementData     Object[10]  (id=189)<br />
        [0]     LinkDiscoveryManager  (id=193)<br />
        [1]     TopologyManager  (id=200)<br />
        [2]     DeviceManagerImpl  (id=207)<br />
        [3]     Firewall  (id=213)<br />
        [4]     LoadBalancer  (id=66)<br />
        [5]     Forwarding  (id=218)<br />
        [6]     null<br />
        ...<br />
`  
事件加入函数

> core/util/ListenerDispatcher.java ==> (71 &#8211; 107) 

<code lang="java" width="600">&lt;br />
//line 38&lt;br />
List&lt;t> listeners = null;&lt;/p>
&lt;p>//line 71&lt;br />
public void addListener(U type, T listener) {&lt;br />
    List&lt;t> newlisteners = new ArrayList&lt;t>();&lt;br />
    if (listeners != null) //listeners列表是否为空(当前监听者列表)&lt;br />
        newlisteners.addAll(listeners);//将原列表中信息复制进来&lt;/p>
&lt;p>    newlisteners.add(listener);&lt;br />
    // Find nodes without outgoing edges&lt;br />
    List&lt;t> terminals = new ArrayList&lt;t>();&lt;br />
    for (T i : newlisteners) {&lt;br />
        boolean isterm = true;&lt;br />
        for (T j : newlisteners) {&lt;br />
            if (ispre(type, i, j)) {&lt;br />
                isterm = false;&lt;br />
                break;&lt;br />
            }&lt;br />
        }&lt;br />
        if (isterm) {&lt;br />
            terminals.add(i);&lt;br />
        }&lt;br />
    }&lt;/p>
&lt;p>    if (terminals.size() == 0) {&lt;br />
        logger.error("No listener dependency solution: " +&lt;br />
        		     "No listeners without incoming dependencies");&lt;br />
        listeners = newlisteners;&lt;br />
        return;&lt;br />
    }&lt;/p>
&lt;p>    // visit depth-first traversing in the opposite order from&lt;br />
    // the dependencies.  Note we will not generally detect cycles&lt;br />
    HashSet&lt;t> visited = new HashSet&lt;t>();&lt;br />
    List&lt;t> ordering = new ArrayList&lt;t>();&lt;br />
    for (T term : terminals) {&lt;br />
        visit(newlisteners, type, visited, ordering, term);&lt;br />
    }&lt;br />
    listeners = ordering;&lt;br />
}&lt;br />
</code>