# Bulk2g_docker
# HARDWARE SETUP
## Hardware setup for calypsoBTS
Hardware setup 1 : Need battery and not programmable with arduino  

[serial_cable](https://osmocom.org/projects/baseband/wiki/Serial_Cable)    [smartspate](https://www.smartspate.com/how-to-create-2g-network-at-your-own-home/)   [sudonull](https://sudonull.com/post/69473-Launching-a-GSM-network-at-home-Pentestit-Blog)
<p align="center">
  <img src="https://github.com/SitrakaResearchAndPOC/GSM_IMSICATCHER_HALFMITM_SPOOFING-SMS-WITH-PHYSICAL-MS/blob/main/usb_motorola.jpg">
</p>



Hardware setup 2 : No need battery and programmable with arduino  
<p align="center">
  <img src="https://github.com/SitrakaResearchAndPOC/GSM_IMSICATCHER_HALFMITM_SPOOFING-SMS-WITH-PHYSICAL-MS/blob/main/USB_TTL.jpg">
</p>

## Hardware setup for USRP

<p align="center" >
  <img width="600" height="200" src="https://github.com/SitrakaResearchAndPOC/BulkSMS_LXD/blob/main/usrp12.jpg">
</p>

<p align="center" >
  <img  width="600" height="200" src="https://github.com/SitrakaResearchAndPOC/BulkSMS_LXD/blob/main/usrp34.jpg">
</p>


# INSTALLATION OF DOCKER KARLIBTS
## preparing docker 
```
docker pull debian:buster
```
```
docker run -tid --privileged -v /dev/bus/usb:/dev/bus/usb -v /dev:/dev -v /tmp/.X11-unix:/tmp/.X11-unix:ro -v $XAUTHORITY:/home/user/.Xauthority:ro --net=host --env="DISPLAY=$DISPLAY" --env="LC_ALL=C.UTF-8" --env="LANG=C.UTF-8" --name bulk2g debian:buster
```
```
xhost +
```
```
docker exec -ti bulk2g /bin/bash
```
```
apt update
```
```
apt install nano zsh vim
```
```
nano /etc/apt/source.list
```
Change apt file
```
#

# deb cdrom:[Debian GNU/Linux 10.13.0 _Buster_ - Official amd64 DVD Binary-1 20220910-18:04]/ buster contrib main

#deb cdrom:[Debian GNU/Linux 10.13.0 _Buster_ - Official amd64 DVD Binary-1 20220910-18:04]/ buster contrib main

# Line commented out by installer because it failed to verify:
#deb http://security.debian.org/debian-security buster/updates main contrib
# Line commented out by installer because it failed to verify:
#deb-src http://security.debian.org/debian-security buster/updates main contrib

# buster-updates, previously known as 'volatile'
# A network mirror was not selected during install.  The following entries
# are provided as examples, but you should amend them as appropriate
# for your mirror of choice.
#
 deb http://deb.debian.org/debian/ buster main contrib
 deb-src http://deb.debian.org/debian/ buster main contrib
```
save by ctrl+x
``` 
apt update
 ```
```
apt-get install nano wget gedit mousepad wireshark
```
```
apt-get install libtool shtool automake dahdi-source libssl-dev sqlite3 libsqlite3-dev libsctp-dev libfftw3-dev libfftw3-3 autoconf libsctp-dev libgnutls28-dev libcurl4-gnutls-dev git-core pkg-config make gcc gcc-arm-none-eabi doxygen libtalloc-dev libpcsclite-dev libusb-1.0-0-dev
```
```
apt-get install build-essential gcc g++ make automake autoconf libtool pkg-config libtalloc-dev libpcsclite-dev libortp-dev libsctp-dev libssl-dev libdbi-dev libdbd-sqlite3 libsqlite3-dev libpcap-dev libc-ares-dev libgnutls28-dev libsctp-dev sqlite3 libsofia-sip-ua-glib-dev libusb-1.0-0-dev libfftw3-dev libgsm1-dev
```
```
apt-get install autoconf automake build-essential ccache cmake cpufrequtils doxygen ethtool g++ git inetutils-tools libboost-all-dev libncurses5 libncurses5-dev libusb-1.0-0 libusb-1.0-0-dev libusb-dev python3-dev python3-mako python3-numpy python3-requests python3-scipy python3-setuptools python3-ruamel.yaml
```
```
apt-get install libtool shtool automake dahdi-source libssl-dev sqlite3 libsqlite3-dev libsctp-dev libfftw3-dev libfftw3-3 autoconf libsctp-dev libgnutls28-dev libcurl4-gnutls-dev git-core pkg-config make doxygen libtalloc-dev libpcsclite-dev libusb-1.0-0-dev
```
```
apt-get install asterisk telnet python3-pip
```
```
pip3 install smpplib
```
Installing dependencies before libosmo-abis
```
apt-get install libortp-dev
```
```
apt-get install fuse zip
```
```
apt-get install libfuse-dev 
```
Creating and installing all components
```
mkdir src
```


Installing UHD
```
cd src 
```
```
git clone --depth 1 -b v3.15.0.0 https://github.com/EttusResearch/uhd
```
```
cd uhd/host
```
```
mkdir build
```
```
cd build
```
```
cmake ..
```
```
make -j4
```
```
make install
```
```
ldconfig
```
```
cd ../../..
```


Installing libosmocore 1.7.0 or 1.0.1
```
apt-get install libmnl-dev
```

```
git clone --depth 1 -b 1.7.0 https://gitea.osmocom.org/osmocom/libosmocore
```
```
cd libosmocore
```
```
autoreconf -fi
```
```
./configure
```
```
make -j4
```
```
make check
```
```
make install
```
```
ldconfig
```
```
cd ..
```
"# 51/51


Just for memos :  
git clone git://git.osmocom.org/osmocom-bb.git  
cd osmocom-bb/  
git checkout 4f677e6ba8434dab376495cd996d140548fa6e93  
cd src  
nano target/firmware/Makefile  
"#uncomment CFLAGS += -DCONFIG_TX_ENABLE in the file target/firmware/Makefile"  
#ctrl+o return ctrl+x  
tail -f target/firmware/Makefile  
make -j4 -e CROSS_TOOL_PREFIX=arm-none-eabi-  
cd ../..  


FOR CALYPSO  
Installing libosmo-dsp
```
git clone git://git.osmocom.org/libosmo-dsp.git
```
```
cd libosmo-dsp/
```
```
git checkout 551b9752bcd5d3d21bb2df0736b1801bda3d0d10
```
```
autoreconf -i
```
```
./configure
```
```
make -j4
```
```
make install
```
```
ldconfig -i
```
```
cd ..
```
Installing trx
```
git clone git://git.osmocom.org/osmocom-bb.git -b fixeria/trx trx
```
```
cd trx/src/
```
```
git checkout 620fe497efa492feff4550e336cc3f8167715936
```
```
nano target/firmware/Makefile
```
"#uncomment CFLAGS += -DCONFIG_TX_ENABLE in the file target/firmware/Makefile"
#ctrl+o return ctrl+x
```
tail -f target/firmware/Makefile
```
```
make -j4 HOST_layer23_CONFARGS=--enable-transceiver -e CROSS_TOOL_PREFIX=arm-none-eabi-
```
```
cd ../..
```


Installing libosmo-abis
```
git clone --depth 1 -b 0.6.0 https://gitea.osmocom.org/osmocom/libosmo-abis
```
```
cd libosmo-abis
```
```
autoreconf -fi
```
```
./configure
```
```
make -j4
```
```
make check
```
```
make install
```
```
ldconfig
```
```
cd ..
```
"# 2/2

Installing libosmo-netif
```
git clone --depth 1 -b 0.4.0 https://gitea.osmocom.org/osmocom/libosmo-netif
```
```
cd libosmo-netif
```
```
autoreconf -fi
```
```
./configure
```
```
make -j4
```
```
make check
```
```
make install
```
```
ldconfig
```
```
cd ..
```
"# 3/3


Installing libosmo-sccp
```
git clone --depth 1 -b 1.0.0 https://gitea.osmocom.org/osmocom/libosmo-sccp
```
```
cd libosmo-sccp
```
```
autoreconf -fi
```
```
./configure
```
```
make -j4
```
```
make check
```
```
make install
```
```
ldconfig
```
```
cd ..
```
"# 5/5


Installing libasn1
```
git clone --depth 1 -b 0.9.31 https://gitea.osmocom.org/cellular-infrastructure/libasn1c
```
```
cd libasn1c
```
```
autoreconf -fi
```
```
./configure
```
```
make -j4
```
```
make check
```
```
make install
```
```
ldconfig
```
```
cd ..
```
"#


Installing libsmpp34
```
git clone --depth 1 -b 1.13.0 https://gitea.osmocom.org/cellular-infrastructure/libsmpp34
```
```
cd libsmpp34
```
```
autoreconf -fi
```
```
./configure
```
```
make -j4
```
```
make check
```
```
make install
```
```
ldconfig
```
```
cd ..
```
"#
```
git clone --depth 1 -b 0.4.0 https://gitea.osmocom.org/cellular-infrastructure/osmo-iuh
```
```
cd osmo-iuh
```
```
autoreconf -fi
```
```
./configure
```
```
make -j4
```
```
make check
```
```
make install
```
```
ldconfig
```
```
cd ..
```
"# 3/3


Installing osmo-ggsn maybe 1.9.0 or 1.3.0
```
git clone --depth 1 -b 1.9.0 https://gitea.osmocom.org/cellular-infrastructure/osmo-ggsn
```
```
cd osmo-ggsn
```
```
autoreconf -fi
```
```
./configure
```
```
make -j4
```
```
make check
```
```
make install
```
```
ldconfig
```
```
cd ..
```
"# 5/5  
Installing osmo-sip-connector 1.3.1 or 1.2.0
```
git clone --depth 1 -b 1.3.1 https://gitea.osmocom.org/cellular-infrastructure/osmo-sip-connector
```
```
cd osmo-sip-connector
```
```
autoreconf -fi
```
```
./configure
```
```
make -j4
```
```
make check
```
```
make install
```
```
ldconfig
```
```
cd ..
```

"#  
Installing osmotrx  1.2.0 or 1.2.2 or 1.0.2 or 1.0.0 
```
git clone --depth 1 -b 1.2.0 https://gitea.osmocom.org/cellular-infrastructure/osmo-trx
```
```
cd osmo-trx
```
```
autoreconf -fi
```
```
./configure --with-uhd
```
```
make -j4
```
```
make check
```
```
make install
```
```
ldconfig
```
```
cd ..
```

"# 5/7

Installing osmobts 1.2.2 or 1.0.0
```
git clone --depth 1 -b 1.2.2 https://gitea.osmocom.org/cellular-infrastructure/osmo-bts
```
```
cd osmo-bts
```
```
autoreconf -fi
```
```
./configure --enable-trx
```
```
make -j4
```
```
make check
```
```
make install
```
```
ldconfig
```
```
cd ..
```
"#8/8


Installing osmo-pcu  0.6.0  or 1.2.0 or 1.1.0 
```
git clone --depth 1 -b 0.6.0 https://gitea.osmocom.org/cellular-infrastructure/osmo-pcu
```
```
cd osmo-pcu
```
```
autoreconf -fi
```
```
./configure
```
```
make -j4
```
```
make check
```
```
make install
```
```
ldconfig
```
```
cd ..
```
"# 12/12
Installing opensc 1.4.1 or 1.3.0
```
git clone --depth 1 -b 1.4.1 https://gitea.osmocom.org/cellular-infrastructure/openbsc
```
```
cd openbsc/openbsc
```
```
autoreconf -fi
```
```
./configure --enable-mgcp-transcoding --enable-nat --enable-smpp --enable-osmo-bsc
```
```
make -j4
```
```
make check
```
```
make install
```
```
ldconfig
```
```
cd ../..
```
"# 15/15

Installing osmo-hlr 1.0.0
```
git clone --depth 1 -b 1.0.0 https://gitea.osmocom.org/cellular-infrastructure/osmo-hlr
```
```
cd osmo-hlr
```
```
autoreconf -fi
```
```
./configure
```
```
make -j4
```
```
make check
```
```
make install
```
```
ldconfig
```
```
cd ..
```
"# 5/5
Installing sgsn 1.6.2 or 1.4.0
```
git clone --depth 1 -b 1.6.2 https://gitea.osmocom.org/cellular-infrastructure/osmo-sgsn
```
```
cd osmo-sgsn
```
```
autoreconf -fi
```
```
./configure
```
```
make -j4
```
```
make check
```
```
make install
```
```
ldconfig
```
```
cd ..
```
```
exit
```

"# 8/8

# Command you need : 
```
dmesg | grep ttyUSB*
```


