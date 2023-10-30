+++
title = "Hardware timestamping"
date = "2023-10-30"

[taxonomies]
tags = ["NIC", "network latency"]
+++

How to measure network latency using hardware timestamps.

<!-- more -->

## Hardware timestamping

Network interfaces become smarter and smarter, being able to execute
functionalities traditionaly managed by the OS. When wanting to develop such a
functionality, a natural question is, "how much latency can I save ?".

Hardware timestamping, an obscure functionality of (recent? Not too old?) NICs,
inserts in a received network packet the current hardware timestamp. If the NIC
clock and host CPU clock are synchronised, it becomes possible to measure the
time it took from the NIC receiving the packet to the OS/application receiving
it, ultimately answering how much latency one can save by offloading a
functionality to the NIC.

With [Arne Vogel](https://sys.cs.fau.de/person/vogel), a PhD student from FAU
Erlangen in Germany with whom I have been working this summer, we have written
a blog article so that everyone can make use of this functionality:

- [In English](https://eng-blog.iij.ad.jp/archives/21198)
- [In Japanese](https://eng-blog.iij.ad.jp/archives/21208)
