---
title: '[转载]First Demonstration of A Quantum Router'
author: richard
layout: post
permalink: /2012/08/05/%e8%bd%ac%e8%bd%bdfirst-demonstration-of-a-quantum-router/
Sidebar-layout:
  - default
categories:
  - 新闻
---
<div id="page1">
  <p>
    转自：<a href="http://www.technologyreview.com/view/428706/first-demonstration-of-a-quantum-router/">http://www.technologyreview.com/view/428706/first-demonstration-of-a-quantum-router/</a>
  </p>
  
  <p>
    Chinese physicists unveil a router that uses a quantum control signal to determine the path of a quantum data signal
  </p>
  
  <p>
    <img title="Quantum router" src="http://www.technologyreview.com/blog/arxiv/files/89588/Quantum%20router.png" alt="" width="450" height="366" /><!--more-->
  </p>
</div>

Physicists have exploited the quantum nature of photons to transmit information for some time now. And in doing so they&#8217;ve discovered just how powerful  quantum communication can be compared to the classical kind.

Instead of sending the 0s and 1s of digital code, quantum communicators can send information in a superposition of states that represent both 0s and 1s at the same time. What&#8217;s more, separate quantum objects such as a pair of photons can be entangled, which means they share the same existence even if they are widely separated. That leads to a form of quantum information that has no classical counterpart.

Quantum information is the enabling factor behind a number of emerging technologies that many physicists expect to have a huge impact on society in future: powerful quantum computers, <a href="http://www.technologyreview.com/view/426699/serious-flaw-emerges-in-device-independent/" target="_blank">(almost)</a> perfectly secure quantum cryptography and the quantum internet that will distribute these capabilities round the planet.

But there&#8217;s a problem with this vision of the quantum future. At the moment, physicists can only send photons carrying quantum information over the length of a single optical fibre.

Guiding the photons into another fibre is a process called routing, which uses a control signal to determine the destination and route of a data signal.  A classical router simply reads the data in the control signal and routes the data signal accordingly.

But in the quantum world, reading a control signal also destroys it. So it&#8217;s only been possible to route quantum data signals using classical control signals. And although that&#8217;s handy, it doesn&#8217;t allow the routing process to exploit the full power of quantum information.

Today, Xiuying Chang and a few buddies at Tsinghau University in China announce that they have built and tested the first quantum router to use a quantum control signal to determine the route of a quantum data signal. &#8220;We&#8230;realize the first proof-of-principle demonstration of a genuine quantum router,&#8221; they say.

In this new device, the information is encoded in the polarisation of photons, either horizontal or vertical. The Chinese group begin by creating a single photon that is in a superposition of both horizontal and vertical polarisation states.

They then convert this single photon into a pair of lower energy photons that are entangled, a process called parametric down conversion. Both of these photons are also in a superposition of polarisation states.

The router works by using the polarisation of one of these photons as the control signal to determine the route of the other, the data signal. The device is simple, little more than a collection of half mirrors for guiding photons and waveplates for rotating their polarisation.

First, let&#8217;s follow the route of the data photon which is determined by a set of half mirrors that send it one way or the other, depending on its polarisation. The trick is to set up the router so that the polarisation of the control photon influences this route.

The Chinese group do this by rotating the polarisation of the control photon using half and quarter wave plates as the data photon reaches the half mirrors. The quantum phenomenon of entanglement then ensures that the data photon is routed accordingly. In effect, the router works like a logic gate.

Of course, the routing success is a probabilistic like all other quantum phenomena. Chang and co finish their experiment by verifying logic-gate like characteristics  of the router and ensuring that both photons are still entangled after passing through it.

That&#8217;s an interesting step forward but the new router has significant limitations. The most significant of these is that it can handle only one quantum bit or qubit at a time. And because the process of parametric down conversion cannot handle more qubits, it cannot be scaled to more qubits.

That&#8217;s a significant drawback. It means that this is a proof-of-principle device but not one that will ever form the basis of a future quantum internet.

In a sense, it&#8217;s a little like the first quantum computers which relied on nuclear magnetic resonance to manipulate the spins of the molecules in a tub of acetone. These performed trivial calculations using a handful of qubits but couldn&#8217;t be scaled up to do anything interesting.

That&#8217;s not to say that we&#8217;ll never have scalable quantum routers. Various groups are working on different approaches that have the potential to scale. Progress is steady but slow.

A quantum internet is coming. The problem is that nobody knows when.

Ref: <a href="http://arxiv.org/abs/1207.7265" target="_blank">arxiv.org/abs/1207.7265</a>: Experimental Demonstration Of An Entanglement-Based Quantum Router