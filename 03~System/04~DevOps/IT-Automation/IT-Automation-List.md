# 自动化资料索引

- [Lessons Learned from Writing Over 300,000 Lines of Infrastructure Code](https://blog.gruntwork.io/5-lessons-learned-from-writing-over-300-000-lines-of-infrastructure-code-36ba7fadeac1)

# 系统设计

- [2018~如何设计一个大规模远程命令执行系统](https://mp.weixin.qq.com/s?__biz=MzUyMzA3MTY1NA==&mid=2247484177&idx=1&sn=570d6025960f668c315b45f11af8ef5b): 简单介绍了百度集群控制系统（Cluster Control System，以下简称 CCS 系统）通过构建两级数据模型、四级调度模型、三级代理执行的方式解决了这些问题，在本篇文章中，我们将续接前文，继续对 CCS 系统的设计实现进行详细剖析。

# OpenSource

## Server Dashboard & Panel

- [2005-htop ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/hishamhm/htop): htop is an interactive text-mode process viewer for Unix systems. It aims to be a better 'top'.

- [Linux Dash ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/afaqurk/linux-dash): A simple & low-overhead web dashboard for linux systems.

- [gtop ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/aksakalli/gtop): System monitoring dashboard for terminal.

- [Glances ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/nicolargo/glances): Glances is a cross-platform monitoring tool which aims to present a large amount of monitoring information through a curses or Web based interface. The information dynamically adapts depending on the size of the user interface.

- [2018~gotop ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/cjbassi/gotop): Another terminal based graphical activity monitor, inspired by gtop and vtop, this time written in Go!

- [osquery ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/facebook/osquery): osquery is an operating system instrumentation framework for OS X/macOS, Windows, and Linux. The tools make low-level operating system analytics and monitoring both performant and intuitive.

- [bashtop ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/aristocratos/bashtop): Linux resource monitor

- [Cockpit ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/cockpit-project/cockpit): Cockpit is an interactive server admin interface. It is easy to use and very light weight. Cockpit interacts directly with the operating system from a real Linux session in a browser.

- [2020~Spug ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/openspug/spug)](https://github.com/openspug/spug): 开源运维平台：面向中小型企业设计的轻量级无 Agent 的自动化运维平台，整合了主机管理、主机批量执行、主机在线终端、文件在线上传下载、应用发布部署、在线任务计划、配置中心、监控、报警等一系列功能。

- [2021~BaoTa ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/aaPanel/BaoTa)](https://github.com/aaPanel/BaoTa): 宝塔 Linux 面板 - 简单好用的服务器运维面板

- [2023~1Panel ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/1Panel-dev/1Panel)](https://github.com/1Panel-dev/1Panel): 1Panel 是一个现代化、开源的 Linux 服务器运维管理面板。

## Container

- [2016~ctop ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/bcicen/ctop): ctop provides a concise and condensed overview of real-time metrics for multiple containers.

- [2017~cAdvisor ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/google/cadvisor): Analyzes resource usage and performance characteristics of running containers.

## Deployment

- [2018~dokku ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/dokku/dokku)](https://github.com/dokku/dokku): Docker powered mini-Heroku. The smallest PaaS implementation you've ever seen.

- [meli ![code](https://ng-tech.icu/assets/code.svg)](https://github.com/getmeli/meli): Open source platform for deploying static sites and frontend applications.

- [2020~Jpom ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/dromara/Jpom)](https://github.com/dromara/Jpom): 简而轻的低侵入式在线构建、自动部署、日常运维、项目监控软件。

- [2022~Goploy ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/zhenorzz/goploy)](https://github.com/zhenorzz/goploy): Devops 项目代码部署发布平台，Deploy, CI/CD, Terminal, Sftp, Server monitor, Crontab Manager, Nginx Manager.

- [2023~MRSK ![code](https://ng-tech.icu/assets/code.svg) ![star](https://img.shields.io/github/stars/mrsked/mrsk)](https://github.com/mrsked/mrsk): MRSK deploys web apps anywhere from bare metal to cloud VMs using Docker with zero downtime. It uses the dynamic reverse-proxy Traefik to hold requests while the new application container is started and the old one is stopped. It works seamlessly across multiple hosts, using SSHKit to execute commands. It was built for Rails applications, but works with any type of web app that can be containerized with Docker.
