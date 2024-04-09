+++
title = "Making Internet Applications Trustworthy"
date = "2024-04-08"

[taxonomies]
tags = ["internet, security, dependability"]
+++

Let's make the Internet a better place!

<!-- more -->

# Context and motivation

"The Internet’s potential is unlimited. As a worldwide resource, the Internet supports commerce,
recreation, research, education, entertainment, and everything in between. But with different
stakeholders and competing demands of the network, safeguarding the future of the Internet can seem
like an impossible task."

-- [The Internet Society](https://www.internetsociety.org/wp-content/uploads/2021/11/Enablers-of-OGST-EN.pdf)

One important aspect to enable the above vision is trustworthiness. This can be
enabled at various levels of the Internet infrastructure, from the low-level
routing infrastructure to the high-level Internet applications. In this project
we are concerned only with the later, high-level Internet applications: with
this project, our goal is is to make Internet applications trustworthy.

# A definition of Trustworthy

In this context, what does trustworthy mean? The Internet Society teaches us
that "a trustworthy Internet meets the expectations of its users by offering a
resilient and reliable base for applications and services".

Trustworthy encompasses several concepts:
- reliability: the service is delivered as promised (e.g., a messaging
  application correctly delivers messages between the participants);
- resilience: the application continues to deliver its service even in the
  presence of errors or malicious behaviours;
- availability: the application is ready to answer users' requests;
- accountability: application operators and users can be identified and held
  responsible for their actions;
- privacy: users can control and understand what information about them is
  collected, how it is collected, and can control how this information is used
  and shared with others. Users might also prefer to remain anonymous. As an
  example, the [GDPR](https://gdpr-info.eu/) is a good example of a regulation
  aimed at protecting users' privacy on the Internet;
- confidentiality: eavesdroppers and attackers cannot observe sensitive data,
  both in transit and at rest;
- integrity: while confidentiality prevents malicious entities to learn
  something, integrity prevents them to alter it, for example a malicious cloud
  storage provider could replace a valid encrypted file with another, valid,
  encrypted file.

# This project

## Purpose

There are different levels where practitioners should increase the trust users
have in the Internet infrastructure, from the low-level routing infrastructure
to the high-level Internet applications. In this project we are concerned only
with the later, high-level Internet applications (web server, database, file
sharing service, etc.).

Our goal is is to make Internet applications trustworthy, i.e.,
- Internet users have guarantees (security, fault tolerance, provided service,
  ...) on the applications they use (e.g., web server, storage service,
  streaming);
- companies running such applications are accountable for their behaviour;
- the Internet is a secure and resilient place without any single point of
  failure or single controlling entity. The Internet has started as a
  decentralized platform, and we want to keep it that way. Centralization not
  only creates single points of failure, but it also enable some companies or
  governments to use everyone's data for their own benefits.

## Approach

Our approach is based on our previous knowledge in fault-tolerance and
security. More precisely, we are working on improving the fault-tolerance and
security of existing Internet applications, both on the server and client side.
Nevertheless, our aim is to empower Internet users: our solutions should
benefits users more than for the companies providing such services.

Security and fault-tolerance are generally costly techniques that can decrease
the performance of an application. We are exploring *practical* solutions that
minimize this overhead so that practitioners can deploy our solutions on the
real Internet without losing their customers.

We are also considering the sustainability of our solutions. With climate
change and international conflicts, it is not absurd to consider a [shortage of
electronic
components](https://en.wikipedia.org/wiki/2020%E2%80%932023_global_chip_shortage),
an [innovation
slowdown](https://www.zdnet.com/article/as-moores-law-slows-high-end-applications-may-feel-the-effect-mit-scientist-warns/)
or [increasing demand on environmental-friendly
solutions](https://news.mit.edu/2022/how-can-we-reduce-carbon-footprint-global-computing-0428).

# Past results

My past research works have addressed this project goal in several ways, as can be seen in the figure below.

![Past research](https://raw.githubusercontent.com/plaublin/plaublin.github.io/main/static/images/2024-04-09_pastresearch.jpg)

Notable projects are:
- RBFT, Next 700 are Byzantine Fault tolerant protocols designed to
  ensure good performance even in the presence of faults, where research works
  usually focuses on improving the performance in the best case scenario where
  no faults occur. The next 700 also empowers clients, as they are able to
  change the behaviour of the protocol if they suspect a fault;
- FullReview makes distributed systems accountable even in the presence of
  selfish participants, i.e., participants that want to maximise their benefits
  without contributing their fare share into the system;
- LibSEAL is a SEcure Auditing Library for internet services. It allows to
  detect integrity violations of internet services without the need to trust
  the service operator, by leveraging a Trusted Execution Environment;
- Endbox is a scalable and secure middlebox framework. It executes middlebox
  functions inside a Trusted Execution Environment on client machines. Despite
  its decentralised model, EndBox's middlebox functions remain maintainable,
  practical and scalable.

# What's next?

Making Internet Applications Trustworthy is a never ending endeavour. We tackle it one step at a time.

Here is a non-exhaustive list of potential sub-projects:
- making Byzantine Fault-Tolerance more practical;
- fault-tolerance for AI systems;
- decentralized and secure Internet;
- securing input devices (keyboard, mouse, etc.) against attacks
  ([badUSB](https://en.wikipedia.org/wiki/BadUSB), [malicious
  cables](https://counterespionage.com/malicious-usb-cables/),
  [keyloggers](https://en.wikipedia.org/wiki/Keystroke_logging));
- novel Trusted Execution Environments;
- combat fake news;
- etc.

Please [keep in touch](mailto:pierrelouis@iij.ad.jp) if you are interested in such projects!
