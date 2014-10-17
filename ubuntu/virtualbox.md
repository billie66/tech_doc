### how to access your VM when you can't connect the network

* add a new adapter (adapter2), select host-only

* get ip address on your host machine

    billie@:~/tech_doc/ubuntu$ ifconfig
    ...
    vboxnet0  Link encap:Ethernet  HWaddr 0a:00:27:00:00:00
    inet addr:192.168.56.1  Bcast:192.168.56.255  Mask:255.255.255.0
    ...

* go to the guest VM to setup network, make the interfaces file look like this

    billie@kitty:/etc/network$ cat interfaces

    # This file describes the network interfaces available on your system
    # and how to activate them. For more information, see interfaces(5).

    # The loopback network interface
    auto lo
    iface lo inet loopback

    # The primary network interface
    auto eth0
    iface eth0 inet dhcp

    # Host-only added by Billie
    auto eth1
    iface eth1 inet static
        address 192.168.56.10
        netmask 255.255.255.0
    billie@kitty:/etc/network$ sudo ifup eth1

* on your host machine

    billie@:~ ssh billie@192.168.56.10

### Enable shared folder

* Open the preferences of the Ubuntu VM (you need to shut it down before) Go to “Shared Folder” and click on “+”

* In the first line of the popup select the folder on your Mac which you want to see in Ubuntu

* In the second line of the popup enter the name “Projects” (or whatever your prefer)

* Activate the second checkbox “automatic mounting” (or a similar wording).

Starting from version 4.0, if you checked this option, shared folder will be
mounted to /media directory automatically, along with prefix "sf_".

* Click “OK” and start your Ubuntu VM

* In Ubuntu (maybe even connected via SSH?) type the following to add a mounting point for the shared folder:
(manual mounting)

    sudo mkdir /mnt/Projects
    sudo chmod 777 /mnt/Projects
    sudo mount -t vboxsf -o uid=1000,gid=1000 Projects /mnt/Projects

Here the automatic mounting point is /media/sf_Projects.

* Now enable auto-mounting. For this, we open the file which is always run at the start of Ubuntu:

    sudo vim /etc/rc.local

maybe use file /etc/fstab, (specified by virtualbox official doc)

* Add the following line above(!!!) the line with “exit 0”:

    sudo mount -t vboxsf -o uid=1000,gid=1000 Projects /mnt/Projects

* save and close vim

* from now on your Mac OS X folder is always in /mnt/Projects inside Ubuntu, even after a reboot

### reference material

* <http://muffinresearch.co.uk/archives/2010/02/08/howto-ssh-into-virtualbox-3-linux-guests/>

* <http://www.lecloud.net/post/52224625343/the-ultimate-setup-guide-ubuntu-13-04-in-virtualbox>

* <http://www.virtualbox.org/manual/ch04.html#sharedfolders>

