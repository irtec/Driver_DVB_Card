# Driver DVB Card
TBS Driver Installation
<br>
1. To install drivers needed root privileges:
<pre>sudo -s</pre>
2. Install system utilities to build drivers from the source code:
<pre>apt-get install build-essential \
    patchutils \
    libproc-processtable-perl \
    linux-headers-`uname –r` \
    git \
    linux-source</pre>
3. Remove old media drivers:
<pre>rm -rf /lib/modules/$(uname -r)/extra
rm -rf /lib/modules/$(uname -r)/kernel/drivers/media
rm -rf /lib/modules/$(uname -r)/kernel/drivers/staging/media</pre>
4. Increase system limits. By the default Linux kernel has limit only for 8 DVB adapters. Change limit before build drivers:
<pre>sed -i.bak -e 's/^\(CONFIG_DVB_MAX_ADAPTERS\)=.*/\1=48/g' /lib/modules/$(uname -r)/build/.config</pre>
5. Disable auto update in Ubuntu 14.04
<pre>sed -i.bak -e 's/^\(APT::Periodic::Update-Package-Lists\).*/\1 "0";/g' /etc/apt/apt.conf.d/10periodic</pre>
6. Disable auto update in Ubuntu 16.04
<pre>systemctl disable apt-daily.service
systemctl disable apt-daily.timer</pre>
7. <b>Install</b>
Downloading and building:
<pre>cd /usr/src
git clone https://github.com/tbsdtv/media_build.git
git clone --depth=1 https://github.com/tbsdtv/linux_media.git -b latest ./media
cd media_build
make dir DIR=../media
make allyesconfig
make -j4
sudo make install</pre>
8. Install firmware for DVB adapters
<pre>cd /usr/src
wget http://www.tbsdtv.com/download/document/linux/tbs-tuner-firmwares_v1.0.tar.bz2
sudo tar jxvf tbs-tuner-firmwares_v1.0.tar.bz2 -C /lib/firmware/</pre>
9. Restart your system
<pre>shutdown -r now</pre>
10. After reboot check adapters
<pre>ls /dev/dvb</pre>
