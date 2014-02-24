---
layout: note
title : "Virtualbox网桥方式联网方法"
categories: "Software"
tags: ["Virtualbox", "Network"]
---

Virtualbox虚拟机用网桥模式上网比较好，记录几个情景。

__情景一__

主机win7 64bit，局域网固定ip接入。Virtualbox中虚拟了一个ubuntu 12.04。

这种情境下，只要把虚拟机的ip设成和真机相同的网段和网关就可以了。

__情景二___

主机win7 64bit，电信宽带pppoe接入。Virtualbox中虚拟了一个ubuntu 12.04。

这种情景要复杂一些。首先选择拨号连接的“属性”，选“共享”选项卡。然后勾选“允许其他用户通过这台电脑的Internet连接”。家庭网络连接选“本地连接”。然后，剩下的两个框也都勾选上。这些设置好后重连一下这个连接，使上面的设置生效。这些都搞定后，看从“本地连接”的“详细属性”中查看IP，再把虚拟机中设置IP为同一网段，网关设为刚刚看到的IP就可以了。
