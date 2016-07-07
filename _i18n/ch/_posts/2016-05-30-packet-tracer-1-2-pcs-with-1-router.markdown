---
layout: post
title: 抓包实验 (2 PC & 1 router)
date: 2016-05-30 04:07:47.000000000 -07:00
type: post
published: true
status: publish
categories: programming
---
Firstly put 2 PCs and 1 router into workspace, use Copper Cross-Over to connect PC and router like the picture 1:

!["screen-shot-2016-05-29-at-8-43-55-pm.png"]({{ site.baseurl }}/assets/screen-shot-2016-05-29-at-8-43-55-pm.png)


For the PC, we need to set its IP address, subnet mask and gateway.

For the router, we need to set the IP address and subnet mask of its 2 interfaces. We also need to turn the port status to be on.

Finally configuration of PCs and router are showed in graphs.

Done! You can try to ping PC1 from PC0 in terminal now.

!["pc1.png"]({{ site.baseurl }}/assets/pc1.png)

!["pc2.png"]({{ site.baseurl }}/assets/pc2.png)



