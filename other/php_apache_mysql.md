I'm a newbie trying to install _PHP_.

I used apt to install _libxml2_, but when I try to configure _PHP_, 
it returns the following error...

    checking whether to enable LIBXML support... yes
    checking libxml2 install dir... no
    configure: error: xml2-config not found. Please check your libxml2 installation.

When I run `locate libxml2`, I can see the following...
    /var/cache/apt/archives/libxml2-dev_2.4.19-4woody1_i386.deb
    /var/cache/apt/archives/libxml2_2.4.19-4woody1_i386.deb
    /var/lib/dpkg/info/libxml2.list
    /var/lib/dpkg/info/libxml2.postrm

A simpler solution is to install _libxml2_ developement packages;
    apt-get install libxml2-dev;

This will fix the dependency issue on debian/ubuntu derivatives.
    apt-get install build-essential;   
