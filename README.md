# Driver DVB Card
TBS Driver Installation
<br>
To install drivers needed root privileges:
<pre>sudo -s</pre>
Install system utilities to build drivers from the source code:
<pre>apt-get install build-essential \
    patchutils \
    libproc-processtable-perl \
    linux-headers-`uname –r` \
    git \
    linux-source</pre>
