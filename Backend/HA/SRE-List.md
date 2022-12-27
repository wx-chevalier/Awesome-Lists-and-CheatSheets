# SRE List

- [So you want to be an SRE?](https://hackernoon.com/so-you-want-to-be-an-sre-34e832357a8c#.x8tn42pb7)

# Overview

- [2018-性能之殇 #Series#](https://lvwenhan.com/%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F/492.html): 本文的目标是在我有限的认知范围内，讨论一下人们为了提高性能做出的种种努力，这里面包含硬件层面的 CPU、RAM、磁盘，操作系统层面的并发、并行、事件驱动，软件层面的多进程、多线程，网络层面的分布式，等等等等。

- [2016-究竟啥才是互联网架构“高可用”](http://6me.us/Fz25N7)

- [2017-大话程序猿眼里的高并发](https://blog.thankbabe.com/2016/04/01/high-concurrency/)：高并发是指在同一个时间点，有很多用户同时的访问 URL 地址，比如：淘宝的双 11，双 12，就会产生高并发, 如贴吧的爆吧，就是恶意的高并发请求，也就是 DDOS 攻击，再屌丝点的说法就像玩撸啊撸被 ADC 暴击了一样, 那伤害你懂得 ( 如果你看懂了，这个说法说明是正在奔向人生巅峰的屌丝。

- [2017-如何提升 Web 后端性能？我的 4 个实践和总结](http://mp.weixin.qq.com/s/KsXS5f-1-217CY5R88qOHQ)：随着互联网的不断发展，日常生活中越来越多的需求通过网络来实现，从衣食住行到金融教育，从口袋到身份，人们无时无刻不依赖着网络，而且越来越多的人通过网络来完成自己的需求。作为直接面对来自客户请求的 Web 服务端，无疑是要同时承受更多的请求，并为用户提供更好的体验。这个时候 Web 端的性能常常会成为业务发展的瓶颈，提升性能刻不容缓。本文作者在开发过程中总结了一些提升 Web 服务端性能的经验，与大家分享。

- [2019-大规模微服务单元化与高可用设计](https://mp.weixin.qq.com/s/5ovOHoI4gZqokez672wriQ): 为了满足以上的要求，这个系统绝不是运维组努力一把，或者开发组努力一把，就能解决的，是一个端到端的，各个部门共同完成的一个目标，所以我们常称为战略设计。

- [2020-School of SRE 🏫](https://github.com/linkedin/school-of-sre): At LinkedIn, we are using this curriculum for onboarding our entry level talents into the SRE role.

## Case Study

- [荔枝 FM 架构师刘耀华：异地多活 IDC 机房架构](http://geek.csdn.net/news/detail/53231)

# Resource

## Book

- [2018-Google Site Reliability Engineering 📚](https://landing.google.com/sre/sre-book/chapters/foreword/): This book shows a willingness to let SRE thinking come out of the shadows.

- [2020-Building Secure & Reliable Systems 📚](https://static.googleusercontent.com/media/landing.google.com/zh-CN//sre/static/pdf/Building_Secure_and_Reliable_Systems.pdf): Best Practices for Designing, Implementing and Maintaining Systems.

## Collection

- [howtheysre ![code](https://martrix-usa.oss-accelerate.aliyuncs.com/logo/code.svg)](https://github.com/upgundecha/howtheysre): A curated collection of publicly available resources on how technology and tech-savvy organizations around the world practice Site Reliability Engineering (SRE).

# Tutorial

- [2022-What every SRE should know about GNU/Linux shell related internals: file descriptors, pipes, terminals, user sessions, process groups and daemons #Series#](https://biriukov.dev/docs/fd-pipe-session-terminal/0-sre-should-know-about-gnu-linux-shell-related-internals-file-descriptors-pipes-terminals-user-sessions-process-groups-and-daemons/): Despite the era of containers, virtualization, and the rising number of UI of all kinds, SREs often spend a significant part of their time in GNU/Linux shells. It could be debugging, testing, developing, or preparing the new infrastructure. It may be the good old bash, the more recent and fancy zsh, or even fish or tcsh with their interesting and unique features.

# OpenSource

## Incidents Management

- [Dispatch ![code](https://martrix-usa.oss-accelerate.aliyuncs.com/logo/code.svg)](https://github.com/Netflix/dispatch): All of the ad-hoc things you're doing to manage incidents today, done for you, and much more!
