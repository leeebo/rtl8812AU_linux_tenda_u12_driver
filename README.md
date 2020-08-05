## 步骤
1. git clone https://github.com/qljz1993/rtl8812AU_linux_tenda_u12_driver.git

2. make

3. sudo make install

4. sudo modprobe 8812au

## 坑1
（make）编译时提示macro "__TIME__" might prevent reproducible builds [-Werror=date-time]
解决方法：打开makefile
```
#将下面这行的注释‘#’去掉
#EXTRA_CFLAGS += -Wno-error=date-time	# Fix compile error on gcc 4.9 and later
```

## 坑2
```
Authentication requested [root] for remove driver:
rmmod: ERROR: Module 8812au is not currently loaded
Authentication requested [root] for insert driver:
insmod: ERROR: could not insert module 8812au.ko: Unknown symbol in module
Authentication requested [root] for install driver:
install -p -m 644 8812au.ko  /lib/modules/4.4.0-161-generic/kernel/drivers/net/wireless/

```
因该是内核版本的问题，需要修改源文件，使用这位老哥的资源可以
https://download.csdn.net/download/qq_20252351/11222555
感谢！

最新版本请参考rtl8812au-master地址https://github.com/gnab/rtl8812au

## ubuntu 18.04 

1. 请参考 https://askubuntu.com/questions/1076771/realtek-0bdaa811-wifi-driver-rtl8812au-on-ubuntu-18-04
2. 如果遇到 WiFi 可以被扫描到，但是需要重复输入密码的情况 （kernel >= 4.15）

[bug 描述](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1852258)

[解决方案](https://askubuntu.com/questions/1149117/tp-link-ac600-archer-t2u-nano-driver-for-ubuntu-18-04/1149288#1149288)

```
sudo apt install git dkms
git clone https://github.com/jeremyb31/rtl8812au-1.git
cd rtl8812au-1
sudo ./dkms-install.sh
```

安全引导将需要被禁用。github repo名称有一点误导，因为源代码支持rtl8812au、rtl8814au和rtl8821au

