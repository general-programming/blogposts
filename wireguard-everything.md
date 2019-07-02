---
title: wireguard everything!
author: linuxgemini
discord: 120267401672523776
date: 2019-07-02
---

We have quite a lot of VMs on our hypervisor and we want to have direct access to those. Unfortunately, we have 3 IP addresses; we can't just assign a new IP to a VM.

I on the other hand, have a lot of virtual servers scattered across Europe and I wanted to make a big network out of it. Sorta like [dn42](https://dn42.net) but without BGP and such (maybe later).

We a total of 7 main nodes:
 - Genprog's Hypervisor,
 - A VDS in Turkey,
 - A Tower Server in my home,
 - A VPS in Netherlands,
 - A VPS in Germany,
 - A VPS in Finland,
 - And a dedicated in Germany that I co-own.

So, [WireGuard](https://www.wireguard.com) time eh?

WireGuard is easy to configure, but this is madness:

![Our mesh network](https://btw.i-use-ar.ch/i/kpz0jb04.png)

Someone can connect to any server, and with some masquerading rules, they can connect to any node they want, through that server.

Job done. I'll probably ramble *more* about this in [my own blog](https://blog.linuxgemini.space).
