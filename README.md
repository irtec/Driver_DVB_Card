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
<pre></pre>
