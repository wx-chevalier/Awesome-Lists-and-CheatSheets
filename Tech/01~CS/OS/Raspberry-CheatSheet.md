# Raspberry CheatSheet | 树莓派资料索引

- 博通 BCM2837B0 SoC，集成四核 ARM Cortex-A53（ARMv8）64 位@ 1.4GHz CPU，集成博通 Videocore-IV GPU
- 内存：1GB LPDDR2 SDRAM
- 有线网络：千兆以太网（通过 USB2.0 通道，最大吞吐量 300Mbps）
- 无线网络:2.4GHz 和 5GHz 双频 Wi-Fi，支持 802.11b/g/n/ac
- 蓝牙：蓝牙 4.2&低功耗蓝牙（BLE）
- 存储：Micro-SD
- 其他接口：HDMI，3.5mm 模拟音频视频插孔，4x USB 2.0，以太网，摄像机串行接口（CSI），显示器串行接口（DSI），MicroSD 卡座，40pin 扩展双排插针
- 尺寸：82mmx 56mmx 19.5mm，50 克

# 安装与配置

## 系统安装

我们首先需要准备 SD 卡并且将系统烧录到其中，在 MAC 系统中，可以通过 df 命令查看分区情况：

```sh
$ df -lh

Filesystem     Size   Used  Avail Capacity iused               ifree %iused  Mounted on
/dev/disk1s1  234Gi  170Gi   60Gi    75% 5903759 9223372036848872048    0%   /
/dev/disk1s4  234Gi  3.0Gi   60Gi     5%       3 9223372036854775804    0%   /private/var/vm
/dev/disk4s1   15Gi  2.4Mi   15Gi     1%       0                   0  100%   /Volumes/NO NAME

# 可选，格式化磁盘
$ sudo diskutil eraseDisk FAT32 CAM_STORE MBRFormat /dev/disk4s1

# 如果提示 Resource Busy，则可进行卸载
$ diskutil unmount /dev/disk4s1

# 烧写系统
$ sudo dd bs=4m if=rpi_35_v6_1_2_3_jessie_kernel_4_4_50.img of=/dev/disk4s1

# 卸载系统
$ diskutil unmountDisk /dev/disk4s1
```

## 系统配置

如果通过 ssh 连接树莓派出现 Access denied 这个提示则说明 ssh 服务没有开启。要手动开启的话，和 WiFi 配置相似，同样在 boot 分区新建一个文件，空白的即可，文件命名为 ssh。注意要小写且不要有任何扩展名。

树莓派在启动之后会在检测到这个文件之后自动启用 ssh 服务。随后即可通过登录路由器找到树莓派的 IP 地址，通过 ssh 连接到树莓派了。

```sh
# 设置 root 账户密码
$ sudo passwd root

# 解锁 root
$ sudo passwd --unlock root

$ su

$ sudo apt-get remove python3-pip; sudo apt-get install python3-pip
```

## 网络配置

用户可以在未启动树莓派的状态下单独修改 /boot/wpa_supplicant.conf 文件配置 WiFi 的 SSID 和密码，这样树莓派启动后会自行读取 wpa_supplicant.conf 配置文件连接 WiFi 设备。

```conf
country=CN
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

# WiFi 使用WPA/WPA2加密
network={
    ssid="WiFi-A"
    psk="12345678"
    key_mgmt=WPA-PSK

    # 连接优先级，数字越大优先级越高（不可以是负数）
    priority=1
}

network={
    ssid="WiFi-B"
    psk="12345678"
    key_mgmt=WPA-PSK
    priority=2

    # 连接隐藏 WiFi 时需要指定该值为 1
    scan_ssid=1
}

#  WiFi 没有密码
network={
    ssid="你的无线网络名称（ssid）"
    key_mgmt=NONE
}

# WiFi 使用WEP加密
network={
    ssid="你的无线网络名称（ssid）"
    key_mgmt=NONE
    wep_key0="你的wifi密码"
}
```

# GPIO

![](https://imgsa.baidu.com/exp/pic/item/9304c888d43f8794e438169fd51b0ef41ad53a78.jpg)

## 输出

```py
import RPi.GPIO as GPIO
import time

def setup():
    GPIO.setmode(GPIO.BOARD)
    GPIO.setup(11, GPIO.OUT)
    GPIO.setup(13, GPIO.OUT)
    GPIO.output(11, GPIO.LOW)
    GPIO.output(13, GPIO.LOW)

def destroy():
    GPIO.output(11, GPIO.LOW)
    GPIO.output(13, GPIO.LOW)
    GPIO.setup(11, GPIO.IN)
    GPIO.setup(13, GPIO.IN)

def openLed():
    setup()
    GPIO.output(13, GPIO.HIGH)
    for i in range(2):
        GPIO.output(11,GPIO.HIGH)
        time.sleep(1)
        GPIO.output(11, GPIO.LOW)
        time.sleep(1)
#    destroy()
    GPIO.cleanup()

if __name__=="__main__":
    openLed()
```

## 输入

![image](https://user-images.githubusercontent.com/5803001/44529356-7d6db780-a71e-11e8-8e9f-ee98249adeee.png)

```py
#!/usr/bin/env python
# encoding: utf-8

import RPi.GPIO
import time

R,G,B=15,18,14

# 按钮输出针脚连接的GPIO口
btnR, btnG, btnB=21,20,16

RPi.GPIO.setmode(RPi.GPIO.BCM)

RPi.GPIO.setup(R, RPi.GPIO.OUT)
RPi.GPIO.setup(G, RPi.GPIO.OUT)
RPi.GPIO.setup(B, RPi.GPIO.OUT)

# 按钮连接的GPIO针脚的模式设置为信号输入模式，同时默认拉高GPIO口电平，
# 当GND没有被接通时，GPIO口处于高电平状态，取的的值为1
# 注意到这是一个可选项，如果不在程序里面设置，通常的做法是通过一个上拉电阻连接到VCC上使之默认保持高电平
RPi.GPIO.setup(btnR, RPi.GPIO.IN, pull_up_down=RPi.GPIO.PUD_UP)
RPi.GPIO.setup(btnG, RPi.GPIO.IN, pull_up_down=RPi.GPIO.PUD_UP)
RPi.GPIO.setup(btnB, RPi.GPIO.IN, pull_up_down=RPi.GPIO.PUD_UP)

try:

	RPi.GPIO.output(R, True)
	RPi.GPIO.output(G, True)
	RPi.GPIO.output(B, True)
	while True:
		time.sleep(0.01)

		# 检测按钮1是否被按下，如果被按下(低电平)，则亮红灯(输出低电平)，否则关红灯
		if (RPi.GPIO.input(btnR) == 0):
			RPi.GPIO.output(R, False)
            print 1
		else:
			RPi.GPIO.output(R, True)

		# 检测按钮2是否被按下，如果被按下(低电平)，则亮绿灯(输出低电平)，否则关绿灯
		if (RPi.GPIO.input(btnG) == 0):
			RPi.GPIO.output(G, False)
            print 2
		else:
			RPi.GPIO.output(G, True)

		# 检测按钮3是否被按下，如果被按下(低电平)，则亮蓝灯(输出低电平)，否则关蓝灯
		if (RPi.GPIO.input(btnB) == 0):
			RPi.GPIO.output(B, False)
            print 3
		else:
			RPi.GPIO.output(B, True)

except KeyboardInterrupt:
	pass

RPi.GPIO.cleanup()
```

# 蓝牙

```sh
# Mini Bluetooth Speaker

$ sudo apt-get update
$ sudo apt-get upgrade

sudo apt-get install pi-bluetooth ( "already the newest version" )

sudo apt-get install blueman pulseaudio pavucontrol pulseaudio-module-bluetooth

sudo reboot

hcitool dev  (look for bluetooth address of the built-in adapter)
             (if don't see it:   sudo hciconfig

bluetoothctl

# devices

# power on

# pairable on

# discoverable on

# scan on

# devices
Device 30:22:12:01:0C:52 Y88

# paired-devices

# agent on

# default-agent

# trust 30:22:12:01:0C:52

# pair 30:22:12:01:0C:52
Attempting to pair with 30:22:12:01:0C:52
[CHG] Device 30:22:12:01:0C:52 Connected: yes
[CHG] Device 30:22:12:01:0C:52 Modalias: usb:v05ACp022Cd0100
[CHG] Device 30:22:12:01:0C:52 UUIDs:
    00001108-0000-1000-8000-00805f9b34fb
    0000110b-0000-1000-8000-00805f9b34fb
    0000110c-0000-1000-8000-00805f9b34fb
    0000110e-0000-1000-8000-00805f9b34fb
    0000111e-0000-1000-8000-00805f9b34fb
    00001124-0000-1000-8000-00805f9b34fb
    00001200-0000-1000-8000-00805f9b34fb
[CHG] Device 30:22:12:01:0C:52 Paired: yes
Pairing successful

# paired-devices
Device 30:22:12:01:0C:52 Y88

# connect 30:22:12:01:0C:52
Attempting to connect to 30:22:12:01:0C:52
[CHG] Device 30:22:12:01:0C:52 Connected: yes

# exit


$ alsamixer  (set volume to 85% - normal)

$ sudo apt-get install omxplayer

$ omxplayer YouBetterRun.mp3
```

```py
import os
import sys
import subprocess
import time

def blue_it():
    status = subprocess.call('ls /dev/input/event0 2>/dev/null', shell=True)
    while status == 0:
        print("Bluetooth UP")
        print(status)
        time.sleep(5)
    subprocess.call('mplayer http://addressToSomeStream.com', shell=True)
        status = subprocess.call('ls /dev/input/event0 2>/dev/null', shell=True)
    else:
        waiting()

def waiting():
    subprocess.call('killall -9 pulseaudio', shell=True)
    time.sleep(2)
    subprocess.call('pulseaudio --start', shell=True)
    time.sleep(2)
    status = subprocess.call('ls /dev/input/event0 2>/dev/null', shell=True)
    while status == 2:
        print("Bluetooth DOWN")
        print(status)
        subprocess.call('~/scripts/autopair', shell=True)
        time.sleep(15)
        status = subprocess.call('ls /dev/input/event0 2>/dev/null', shell=True)
    else:
        blue_it()

blue_it()
```
