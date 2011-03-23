How to install virtualbox in ubuntu 9.04 as user account

sudo apt-get install dkms

Download virtualbox-3.0_3.0.8-53138_ubuntu_jaunty_i386.deb

sudo dpkg -i ~.deb)

Note, during installing will occur errors if your os does't contain libcurl3, so you should install libcurl3 first that is very simply in ubuntu just using command line (apt-get install libcurl3)

When installing libcurl3 some errors occur,for example, 'Could not get lock /var/cache/apt/archives/lock' resulting in libcurl3 can't install completely.

In order to resolve this problem, you just delete this file /var/cache/apt/archives/lock

Ok, then virtualbox can be installed in ubuntu.

In addition, you must install following packages before installing virtualbox. Qt 4.3.0 or higher SDL 1.2.7 or higher (This graphics library is typically called libsdl or similar)

I only installed Qtcreator.And, ubuntu 9.04 has installed libsdl already.

If virtualbox was installed successfully, then you can run it though Applications-System Tools-sun VirtualBox.

I use windows 7 to test if VirtualBox can run correctly.Good, windows 7 guest os can be installed.

You can get help from http://www.virtualbox.org/manual/UserManual.html#startingvboxonlinux
