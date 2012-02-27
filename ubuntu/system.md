### how to change GNOME focus policy 

In ubuntu, the default focus policy of GNOME is "click to focus", which means 
a window become active you need to click on it, but I want to change it to 
"focus follows mouse", which means a window get focus by the mouse passing 
over it. So this will ease text copying and pasting.

    System->windows->select windows when the mouse moves over them

### how to check the bits of OS

    uname -a
    
For example i[3456]86 are 32-bit, while X86\_64 is 64-bit.

### how to see whether the cpu is 32-bit or 64-bit

    grep --color=always -iw lm /proc/cpuinfo
    
If this command returns "lm" (Long Mode), then your processor is capable of
64-bit. 

### make a bootable usb stick 

    System->Administration->Startup Disk Creator 
