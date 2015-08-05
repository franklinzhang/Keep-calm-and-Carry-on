#UHD安装
安装方式：手动编译
## 安装依赖包

    sudo apt-get install libboost-all-dev libusb-1.0-0-dev python-cheetah doxygen python-docutils cmake
## 编译安装
下载源码

    git clone git://github.com/EttusResearch/uhd.git
如果要FPGA的源码，也可以一起下载

    git clone --recursive git://github.com/EttusResearch/uhd.git
编译安装

    cd /uhd/host
    sudo mkdir build
    cd build
    cmake ../
    make
    make test
    sudo make install
    sudo ldconfig
可以使用lsusb看ubuntu是否识别usrp
接下来添加gnuradio

    sudo addgroup usrp
    sudo usermode -G usrp -a <YOURNAME>
    echo 'ACTION=="add", BUS=="usb", SYSFS{idVendor}=="fffe", SYSFS{idProduct}=="0002", GROUP:="usrp", MODE:="0660"' > tmpfile
    sudo chown root.root tmpfile
    sudo mv tmpfile /etc/udev/rules.d/10-usrp.rules
重新加载usrp

    sudo udevadm control --reload-rules
使用以下命令查看usrp

    ls -lR /dev/bus/usb | grep usrp
