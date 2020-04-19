# Driver DVB Card
TBS Driver Installation
<br>
<b>1. Prepare system</b>
<p>- To install drivers needed root privileges:</p>
<pre>sudo -s</pre>
<p>- Install system utilities to build drivers from the source code:</p>
<pre>apt-get install build-essential \
    patchutils \
    libproc-processtable-perl \
    linux-headers-`uname –r` \
    git \
    linux-source</pre>
<p>- Remove old media drivers:</p>
<pre>rm -rf /lib/modules/$(uname -r)/extra
rm -rf /lib/modules/$(uname -r)/kernel/drivers/media
rm -rf /lib/modules/$(uname -r)/kernel/drivers/staging/media</pre>
<p>- Increase system limits. By the default Linux kernel has limit only for 8 DVB adapters. Change limit before build drivers:</p>
<pre>sed -i.bak -e 's/^\(CONFIG_DVB_MAX_ADAPTERS\)=.*/\1=48/g' /lib/modules/$(uname -r)/build/.config</pre>
<b>2. Disable auto update in Ubuntu 14.04</b>
<pre>sed -i.bak -e 's/^\(APT::Periodic::Update-Package-Lists\).*/\1 "0";/g' /etc/apt/apt.conf.d/10periodic</pre>
<b>3. Disable auto update in Ubuntu 16.04</b>
<pre>systemctl disable apt-daily.service
systemctl disable apt-daily.timer</pre>
<b>4. Install</b>
<p>- Downloading and building:</p>
<pre>cd /usr/src
git clone https://github.com/tbsdtv/media_build.git
git clone --depth=1 https://github.com/tbsdtv/linux_media.git -b latest ./media
cd media_build
make dir DIR=../media
make allyesconfig
make -j4
sudo make install</pre>
or
<pre>mkdir ljalves-tbsdriver
cd ljalves-tbsdriver
git clone https://github.com/ljalves/media_build.git
git clone --depth=1 https://github.com/ljalves/linux_media.git -b latest ./media
cd media_build
make dir DIR=../media
make distclean
make
sudo make install</pre>
<p>- Install firmware for DVB adapters</p>
<pre>cd /usr/src
wget http://www.tbsdtv.com/download/document/linux/tbs-tuner-firmwares_v1.0.tar.bz2
sudo tar jxvf tbs-tuner-firmwares_v1.0.tar.bz2 -C /lib/firmware/</pre>
<p>- Restart your system</p>
<pre>shutdown -r now</pre>
<p>- After reboot check adapters</p>
<pre>ls /dev/dvb</pre>
<p>#Automatic Install</p>
<pre>curl https://raw.githubusercontent.com/irtec/Driver_DVB_Card/master/drv-tbs.sh | bash</pre>
