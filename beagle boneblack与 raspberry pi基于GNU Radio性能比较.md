# beagle boneblack与 raspberry pi基于GNU Radio性能比较

标签： bbb pi2 gnuradio

---
##一.基本介绍

###1.beagle boneblack介绍
beagle boneblack是beagle board家族中的一员（以下简称bbb）
![bbb配置图][1]
![bbb实物图][2]
![各接口标识][3]
###2.raspberry pi介绍
raspberry pi，我们俗称树莓派，或者卡片电脑，我们这里对比的是树莓派二代。
![树莓派二代实物图][4]
下面是树莓派二代的比较重要配置
1. Broadcom BCM2836 ARMv7处理器，900MHZ
2. 1G LPDDR2 SDRAM
3. 完全兼容之前的 PI （A/B A+ B+）
4. 40pin GPIO
5. 以太网接口等等

##二.在使用GNU Radio方面比较

###1.系统支持
| bbb                           | raspberry pi                     |  
| -------------                 |:-------------:                   | 
| Debian, Android, FreeBSD等等  | NOOBS, RASPBIAN, UBUNTU MATE,等等|
###2.相关项目
首先是再bbb上的sdr，有一个专门的带有gnuradio的ubuntu14.04镜像，[这是镜像链接][5]，使用这个镜像之后，再bbb上安装其他的sdr软件会很轻松，下面是镜像中的相关资源列表：

 1. GNU Radio3.7
 2. keenerd’s rtlsdr bundle
 3. gqrx
 4. multimode (having issues compiling, will contact author. Prob compatibility issues with gnuradio 3.7)
 5. LTE-Cell-Scanner
 6. LTE-Tracker
 7. multimon – Pogsac Pager Decoder
 8. rtl_flex_noX – Flex Pager Decoder
 9. SuperKuh’s Dongle Logger – pyrtlsdr – Fast version
 10. rtl_433
 11. SDR-J
 12. rtl_sdr wide spectrum analyzer
 13. DSD 1.7
 14. RTLAMR
 15. RTL_FM_Python

可以看出bbb已经有现成的资源，在sdr方面的支持很广，如果使用bbb运行gnuradio没有任何压力
接下来是树莓派二代的，之前的树莓派B+版本，是不能运行gnuradio的，现在树莓派二代有四核处理器，1G的RAM，几乎是之前性能的几倍，我们用它来运行一下SDR应用。
a. 首先是安装gnuradio
安装gnuradio就是要安装gnuradio本身的代码库，以及相关依赖包的代码，这里在使用apt-get安装之前，我们需要进行一点设置

     sudo nano /etc/apt/sources.list
加行一行

    deb http://archive.raspbian.org/raspbian jessie main
接下来

    sudo apt-get update
    sudo apt-get install gnuradio gnuradio-dev
这样gnuradio就安装好了。
b.设置RTL-SDR，运行一些sdr应用

    sudo /etc/modprobe.d/raspi-blacklist.conf
加上一行

    blacklist dvb_usb_rtl28xxu
接下来

    sudo apt-get install rtl-sdr gr-osmosdr
    lusb
就可以看到你的rtlsdr设备，接下来设置设备参数

     sudo nano /etc/udev/rules.d/20.rtlsdr.rules
     SUBSYSTEM=="usb", ATTRS{idVendor}=="0bda", ATTRS{idProduct}=="2832", GROUP="adm", MODE="0666", SYMLINK+="rtl_sdr"
运行一个简单的例子

    osmocom_fft
![简单测试][6]

总体来说，树莓派二代，无论是安装gnuradio还是运行一些相关应用都没有问题，其他例子，例如[在树莓派2上跑GSM][7]

##三.结果
通过各个已有项目可以看出，bbb在sdr方面没有任何问题，树莓派2在之前几代树莓派的基础上，性能有很大提升，在sdr方面还有待验证，但是对于sdr的支持没有任何问题，接下来我们需要考虑的就是用途以及经济因素。
bbb的价格为 52.7$
树莓派2的价格为42.4$
主要看用途，如果只是简单的跑gnuradio上的一些例子（GSM已经可以在树莓派上搞定了）还是选择树莓派，因为树莓派相关资源多，也就是使用树莓派的活跃社区比较多，如果在gnuradio上运行的应用需要很高的处理能力，或者进行商用，或者在开发板周围连接很多外设传感器的话，最好选择bbb。

    

 
 


  [1]: http://elinux.org/images/2/2b/Features.jpg
  [2]: http://elinux.org/images/2/23/REV_A5A.jpg
  [3]: http://elinux.org/images/a/a7/COMP_A5A.jpg
  [4]: http://ecx.images-amazon.com/images/I/4133JwedpXL.jpg
  [5]: http://www.kd0cq.com/2014/08/packed-full-beaglebone-black-img-file-rtl-sdr-gnuradio-gqrx-lots-more-on-ubuntu-14-04/
  [6]: http://www.rs-online.com/designspark/assets/ds-assets/uploads/images/54cf411e70f44f6fa1f14cfe0ab56371osmocom_fft.jpg
  [7]: http://www.rs-online.com/designspark/electronics/eng/blog/running-a-gsm-network-on-the-raspberry-pi-2
