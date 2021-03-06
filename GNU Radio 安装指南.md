# GNU Radio安装指南(操作系统：Ubuntu 14.04)
本文档采用手动编译方式安装,不使用 apt-get 方式安装，即

    apt-get intall gnuradio
的方式，如果之前使用此方式安装过gnuradio，使用

    sudo apt-get remove gnuradio
    
将gnuradio卸载.

安装分为两步，首先安装依赖包，依赖包安装成功再手动编译gnuradio
## 1.安装依赖包
我们需要以下这些依赖包
#### 开发工具
。g++

。git

。make

。cmake

。sdcc

。guile

。ccache(经常编译的话建议安装)

#### 运行和编译需要的库
。Python-dev

。SWIG

。FFTW 3.X(libfftw3-dev)

。cppunit(libcppunit-dev)

。Boost 1.35 (or later, but not 1.46, 1.47 or 1.52)

。GSL GNU Scientific Library (libgsl0-dev)

。libusb and libusb-dev

。ALSA (alsa-base, libasound2 and libasound2-dev)

#### grc

。python-numpy

。python-cheetah

。python-lxml

#### WX GUI

。python-wxgtk2.8 

。python-numpy

#### QT GUI

。PyQT4

。PyQwt5

。QT-OpenGL

。Fontconfig

。python-qt4

。python-qwt5-qt4

。libqt4-opengl-dev

。libqwt5-qt4-dev

。libfontconfig1-dev

。libxrender-dev

。libxi-dev

#### 一些其他的依赖包

。libsdl1.2-dev

。python-scipy

。python-matplotlib

。python-tk

。doxygen

。octave

在安装依赖之前先更新软件源

    sudo apt-get update
接下来安装上述依赖包，下面命令可以直接复制运行

    sudo apt-get -y install git-core cmake g++ python-dev swig  pkg-config libfftw3-dev libboost1.55-all-dev libcppunit-dev libgsl0-dev  libusb-dev libsdl1.2-dev python-wxgtk2.8 python-numpy  python-cheetah python-lxml doxygen libxi-dev python-sip  libqt4-opengl-dev libqwt-dev libfontconfig1-dev libxrender-dev  python-sip python-sip-dev
这个是官方给的依赖包，版本更新有可能会缺少一些依赖包，所以最好把下面两组命令也运行一下，
第一个

    sudo apt-get -y install libfontconfig1-dev libxrender-dev libpulse-dev \ swig g++ automake autoconf libtool python-dev libfftw3-dev \ libcppunit-dev libboost-all-dev libusb-dev fort77 sdcc sdcc-libraries \ libsdl1.2-dev python-wxgtk2.8 git guile-1.8-dev \  libqt4-dev python-numpy ccache python-opengl libgsl0-dev \ python-cheetah python-lxml doxygen qt4-dev-tools \  libqwt5-qt4-dev libqwtplot3d-qt4-dev pyqt4-dev-tools python-qwt5-qt4

第二个

    sudo apt-get -y install build-essential cmake git-core autoconf automake  libtool g++ python-dev swig pkg-config libfftw3-dev libboost1.53-all-dev libcppunit-dev libgsl0-dev libusb-dev sdcc libsdl1.2-dev python-wxgtk2.8 python-numpy python-cheetah python-lxml doxygen python-qt4 python-qwt5-qt4 libxi-dev libqt4-opengl-dev libqwt5-qt4-dev libfontconfig1-dev libxrender-dev libusb-1.0
接下来设置环境变量PYTHONPATH

    exportPYTHONPATH=/opt/qt/lib/python2.7/dist-package
## 2.安装gnuradio
首先下载源码，可以翻墙的直接用

    git clone --recursive http://git.gnuradio.org/git/gnuradio.git
或者

    git clone --recursive git://git.gnuradio.org/gnuradio.git
不能翻墙的就使用

    git clone https://github.com/gnuradio/gnuradio
    
    cd gnuradio
    
    git clone https://github.com/gnuradio/volk
下载好源码之后，开始编译,进入gnuradio目录

    cd gnuradio
    sudo mkdir build
    cd build
    cmake ../
    make
一般在这里，如果依赖包安装不全的话，会在cmake这一步出现问题，这时仔细看错误提示信息，缺少什么依赖就安装什么，安装完之后，重新camke，这一段会花很长时间。
完成之后，检查一下

    sudo make test
检查100%通过之后，安装

    sudo make install
这样，gnuradio就安装完成了，可以使用gnuradio-companion启动。
