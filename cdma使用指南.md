# CDMA Module使用指南

标签（空格分隔）： cdma

---

在使用本指南之前，请确认在安装Gnuradio时，所有的依赖库都已安装完毕，详见[这里][1]

step1：安装，首先进入自己需要安装的目录，例如/home/mpj等，自行选择

    git clone https://github.com/anastas/gr-cdma.git
clone好之后，编辑gr-cdma/python/cdma_parameters.py的第97行，把prefix设置为你的cdma所在的目录，例如我使用上面的目录就是

    prefix=/home/mpj/gr-cdma
step2：编译
回到/home/mpj目录下，

    sudo mkdir build_cdma
    cd build_cdma
    cmake ../gr_cdma
    make
    sudo make install
    sudo ldcondig
step3：添加模块
在上面步骤都成功完成之后，

    cd gr-cdma/apps
    sudo gnuradio-companion &
然后先添加子模块：

    amp_var_est_hier.grc",

    "cdma_tx_hier.grc",

    "chopper_correlator.grc",

    "cdma_rx_hier.grc",

    "cdma_tx_hier1.grc",

    "cdma_rx_hier1.grc"
每个在添加之后都generate一遍，运行一边，
注意*************************************************************************
在rx_fier模块中缺少一个import，我们需要自己添加import numpy，否者会不能generate和运行。

step4：最后一步
在上面步骤都完成之后，我们可以加载txrx的grc或者txrx1的grc进行仿真，如果有两个USRP的话，可以分别加载tx和rx的grc，注意设置uarp的地址，可以使用uhd_find_devices来看usrp设备的地址，到这里就可以直接使用cdma module了。


TIPS:如果需要修改参数的话，打开/gr-cdma/python/cdma_parameters.py进行修改，修改之后需要重新编译一下就可以了。

****************************************注意****************************************
如果出现在启动gnuradio-companion时无法加载模块，我们需要修改一个参数

    sudo nano /etc/gnuradio/conf.d/grc.conf
设置local_blocks_path= /home/mpj/gr-cdma/apps(这里应该是你的gr-cdma的路径)


  [1]: https://github.com/VNDJ/Keep-calm-and-Carry-on/blob/master/GNU%20Radio%20%E5%AE%89%E8%A3%85%E6%8C%87%E5%8D%97.md
