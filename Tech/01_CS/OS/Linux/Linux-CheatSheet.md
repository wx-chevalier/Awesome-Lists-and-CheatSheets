# Linux CheatSheet

BIOS：

Basic Input Output System 的缩略词，直译"基本输入输出系统"。

它是一组固化到计算机内主板上一个 ROM 芯片上的程序，它保存着计算机最重要的基本输入输出的程序、开机后自检程序和系统自启动程序，它可从 CMOS 中读写系统设置的具体信息。其主要功能是为计算机提供最底层的、最直接的硬件设置和控制。

GRUB：

GRand Unified Bootloader 简称“GRUB”，是一个来自 GNU 项目的多操作系统启动程序。

UEFI

Unified Extensible Firmware Interface，全称“统一的可扩展固件接口”

是一种详细描述类型接口的标准。这种接口用于操作系统自动从预启动的操作环境，加载到一种操作系统上。

可扩展固件接口（Extensible Firmware Interface，EFI）是 Intel 为 PC 固件的体系结构、接口和服务提出的建议标准。其主要目的是为了提供一组在 OS 加载之前（启动前）在所有平台上一致的、正确指定的启动服务，被看做是有近 20 多年历史的 BIOS 的继任者。UEFI 是由 EFI1.10 为基础发展起来的，它的所有者已不再是 Intel，而是一个称作 Unified EFI Form 的国际组织。

# Systemd

[init 进程](./Linux-CheatSheet.md)是 Linux 系统 Booting 之后的首个进程，其作为守护进程运行直至系统关闭；传统的 Linux 中的服务控制方式也主要依赖于 sysvinit 机制:

```sh
$ sudo /etc/init.d/apache2 start
# 或者
$ service apache2 start
```

当 sysvinit 系统初始化的时候，它是串行启动，并且会将所有可能用到的后台服务进程全部启动运行；系统必须等待所有的服务都启动就绪之后，才允许用户登录，导致启动时间过长与系统资源浪费。并且 init 进程只是执行启动脚本，不管其他事情，脚本需要自己处理各种情况，使得脚本复杂度增加很多。Systemd 就是为了解决这些问题而诞生的。它的设计目标是，为系统的启动和管理提供一套完整的解决方案。

![image](https://user-images.githubusercontent.com/5803001/45408944-64fb1800-b6a0-11e8-97a3-83bb4c681aff.png)

# 用户进程

Linux 在操作这些物理内存时，不会直接操作物理内存，而是建立一个虚拟地址（可以理解成跟物理内存相对应的映射），即在物理内存跟进程之间增加一个中间层。

系统将虚拟地址分为两部分：一部分专门给系统内核使用，另一部分给用户进程使用。对于 32 位的系统，虚拟地址范围是 0x00000000 ~ 0xFFFFFFFF，即最大虚拟内存为 2^32 Bytes = 4GB，系统将最高的 1G 字节（从虚拟地址 0xC0000000 到 0xFFFFFFFF）分配内核使用，此区域称作内核空间；另外将较低的 3G 字节（从虚拟地址 0x00000000 到 0xBFFFFFFF），供各个进程使用，称为用户空间。由于虚拟地址是物理内存的映射，相当于系统将物理内存分成两部分单独使用。所以，现在有两个概念：

内核空间：系统内核使用的内存空间；当一个进程执行调用系统命令(例如 read, write)时，会进入内核代码的执行，进程此时的状态我们称之为内核态。
用户空间：用户进程使用的内存空间；当一个进程执行用户自己的代码时，该进程此时的状态为用户态。

# Links

- https://www.ibm.com/developerworks/cn/linux/1407_liuming_init3/index.html
