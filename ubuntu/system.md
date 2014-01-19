### change GNOME focus policy

In ubuntu, the default focus policy of GNOME is "click to focus", which means 
a window become active you need to click on it, but I want to change it to 
"focus follows mouse", which means a window get focus by the mouse passing 
over it. So this will ease text copying and pasting.

    System->windows->select windows when the mouse moves over them

### check the bits of OS

    uname -a

For example i[3456]86 are 32-bit, while X86\_64 is 64-bit.

### see whether the cpu is 32-bit or 64-bit

    grep --color=always -iw lm /proc/cpuinfo

If this command returns "lm" (Long Mode), then your processor is capable of
64-bit.

### make a bootable usb stick

    System->Administration->Startup Disk Creator 

### check what ports are open

    nmap -sS -O 127.0.0.1

or:

    netstat -ntulp

### list all the users

    lastlog

### add/delete a new account

    sudo adduser username --ingroup admin

    sudo deluser username

You should remove the user's home directory manually.

<https://help.ubuntu.com/11.04/serverguide/user-management.html>

### list all the groups which a user belongs to

    groups username

### list the members in a group

    members()
    {
        cat /etc/group | grep --regex "^$1:.*" | awk -F: '{print $4}'
    }
    members group

or:

    sudo apt-get install members
    members group

### chkconfig (ubuntu 12.04)

start ssh server, meet error like below:

    $ chkconfig -s ssh on
    /sbin/insserv: No such file or directory

fix it with this command:

    $ ln -s /usr/lib/insserv/insserv /sbin/insserv

### how to stop being prompted to unlock the keyring

http://askubuntu.com/questions/31786/chrome-asks-for-password-to-unlock-keyring-on-startup
