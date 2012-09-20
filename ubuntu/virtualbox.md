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

### reference material

<http://muffinresearch.co.uk/archives/2010/02/08/howto-ssh-into-virtualbox-3-linux-guests/>
 
