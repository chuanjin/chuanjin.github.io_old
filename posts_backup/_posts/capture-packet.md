layout: capture
title: Capture Network Packet
date: 2017-03-04 14:10:44
tags: [Tools]
categories: R&D
---

Tcpdump is a very useful tool to capture network packets.
e.g. to capture TCP packet from interface lo0 via port 9999

```
sudo tcpdump -i lo0 port 9999 -XX -v
```
<!--more-->

Here demostrate sending some UDP packets, using tcpdump to capture them and using Tcpreplay to playback.

1. Send some UDP packets via port 9999
![](/images/udps.png)
2. Listen UDP packets from port 9999
![](/images/udpl.png)
3. Capture UDP packet using Tcpdump, save captured packets into a file
![](/images/tcpdump_udp.png)
4. Playback captured packets
![](/images/tcpreplay_udp.png)
5. Listen UDP packets to verify
![](/images/udpl2.png)


Let's have more fun! Assuming we have captured some UDP packets using the command below:

```
sudo tcpdump -i en0 udp port 3333 -XX -v -w li.pcap
```

Then we use tcprewrite command to reverse the source and destination.

![](/images/final.png)

And if we double check the modified .pcap file, it shows as we want.
![](/images/reversed.png)

I also wrote a shell script to rewrite the network package automatically.
{% gist chuanjin/d0fa3bc5b90e15fd14354731dd0c7a7a  %}


references:
http://xmodulo.com/how-to-capture-and-replay-network-traffic-on-linux.html
http://rationallyparanoid.com/articles/tcpdump.html
https://danielmiessler.com/study/tcpdump/#gs.Xztynp0
http://www.jianshu.com/p/5334025cfb5e
