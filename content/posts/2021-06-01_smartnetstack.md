+++
title = "SmartNetStack project"
date = "2021-06-01"

[taxonomies]
tags = ["smartNIC"]
+++

Let's execute the network stack on a smartNIC to improve the performance of
network applications

<!-- more -->

## SmartNetStack: Network Stack Offloading on SoC-based smartNIC

PI: [Pierre Louis Aublin](https://www.iijlab.net/en/members/pierrelouis.html),
IIJ Innovation Institute

In today's architectures, cloud applications (such as web servers, key-value
stores or databases) execute both the application logic and the network stack
on the host CPU. As network speeds increase to more than 100Gbps, this becomes
inefficient: when executing the Redis key-value store on a 40Gbps network, more
than 38% of the CPU cycles are dedicated to TCP/IP processing [MOON20]; this
increases as the network speed increases.

Network vendors now propose smartNICs, special network cards that embed
additional hardware functionalities for custom packet processing, cryptographic
operations, checksum computation, and so on. Recent smartNICs, such as the
SoC-based Mellanox BlueField smartNICs, are drawing the attention of
researchers [KIM20, LIU21] thanks to their flexibility and ease-of-programming.

Researchers have successfully offloaded parts of the network stack to the
smartNIC [LE17, KIM20, MOON20]. However, offloading the entire network stack is
believed to be impractical due to hardware limitations, performance and
security issues, and so on [MOGUL03, PISMENNY21].

In this project we would like to challenge this assumption and explore the
performance of cloud applications when the entire network stack is offloaded to
the smartNIC, in particular the TCP/IP stack. The benefits are multiple: better
CPU utilization by the application logic, lower network latency, better DMA
bandwidth utilization, and better energy efficiency.

This project is divided into three steps: (i) measure the design and
performance characteristics of user-level network stacks such as DPDK-ANS
[ANS21], mTCP [JEONG14] or lwIP [DUNKELS01]; (ii) develop a fast DMA library to
efficiently send application payload between the smartNIC and the host
application; and (iii) propose a novel programming interface for applications
to make efficient use of this architecture.

In the first step we will extend the analysis performed by Liu et al. [LIU21]
on BlueField-2 smartNICs by measuring the design and performance
characteristics of user-level network stacks such as DPDK-ANS [ANS21], mTCP
[JEONG14] or lwIP [DUNKELS01]. Liu et al.'s network analysis focused only on
the Linux kernel network stack, which is inefficient as it involves expensive
system calls.

In a second step, we will develop a fast DMA library to efficiently send
application payload between the smartNIC and the host application. As the
network stack is entirely executed on the smartNIC, the application payload can
be directly sent to the application. This removes metadata (such as the IP and
TCP headers), increases the data transferred size (as small network packets are
aggregated on the smartNIC), and improves the DMA bandwidth utilization.

Finally, we will propose a novel programming interface for applications to make
efficient use of this architecture. Application developers do not need to rely
on the socket API anymore. In particular network-related code (for example to
manage connections or re-transmit messages) is moved to the smartNIC, with the
application only receiving and sending its specific payload to the smartNIC.

This project will leverage the BlueField-2 smartNICs available at CloudLab. We
will first focus on one applications: the Nginx web server [NGINX21]. We will
measure the application performance, network throughput, latency (including
average and tail latency), CPU usage, DMA bandwidth, and so on. Extensions to
this work are multiple: optimizing the performance of other types of
applications (key-value store, databases, machine learning, etc.); offloading
additional network functionalities (in particular TLS), etc.

## Publications


- **A Secure Network Stack for the Untrusted Cloud**. Keita Aihara, Pierre-Louis Aublin, and Kenji Kono. In the Fifteen European Conference on Computer Systems (EuroSys). April 2020.
- **secureTCP: Securing the TCP/IP stack using a Trusted Execution Environment**. Keita Aihara, Pierre-Louis Aublin, and Kenji Kono. In the Information Processing Society of Japan System Software and Operating System conference (ComSys). December 2019.

## References

- [ANS21] ANS team, "ANS: DPDK Native Accelerated Network Stack," 2021. Available: http://www.ansyun.com/
- [DUNKELS01] Dunkels, Adam. "Design and Implementation of the lwIP TCP/IP Stack." Swedish Institute of Computer Science 2.77 (2001).
- [JEONG14] Jeong, EunYoung, et al. "mtcp: a highly scalable user-level {TCP} stack for multicore systems." 11th {USENIX} Symposium on Networked Systems Design and Implementation ({NSDI} 14). 2014.
- [KIM20] Kim, Duckwoo, SeungEon Lee, and KyoungSoo Park. "A Case for SmartNIC-accelerated Private Communication." 4th Asia-Pacific Workshop on Networking. 2020.
- [LE17] Le, Yanfang, et al. "UNO: Uniflying host and smart NIC offload for flexible packet processing." Proceedings of the 2017 Symposium on Cloud Computing. 2017.
- [LIU21] Liu, Jianshen, et al. "Performance Characteristics of the BlueField-2 SmartNIC." arXiv preprint arXiv:2105.06619 (2021).
- [MEMCACHED21] Memcached team, "High-performance, distributed memory object caching system." 2021. Available: https://memcached.org/
- [MOGUL03] Mogul, Jeffrey C. "TCP Offload Is a Dumb Idea Whose Time Has Come." HotOS. 2003.
- [MOON20] Moon, YoungGyoun, et al. "Acceltcp: Accelerating network applications with stateful TCP offloading." 17th USENIX Symposium on Networked Systems Design and Implementation (NSDI 20). 2020.
- [NGINX21] Nginx team, "Nginx: High performance Load Balancer, Web Server & Reverse Proxy." 2021. Available: https://www.nginx.com/
- [PISMENNY21] Pismenny, Boris, et al. "Autonomous NIC offloads." Proceedings of the 26th ACM International Conference on Architectural Support for Programming Languages and Operating Systems. 2021. 
