### enable wireless network in ubuntu 10.10

My laptop is Dell vostro 1088, which installed ubuntu 10.10. It is surprising
that wireless network can not work after I use it several days. I don't know
how to handle the problem. So I think I should reinstall the ubuntu 10.10. It
is so bad that my machine still can not connect to the wireless network and
not detect any wireless signal. Then I asked google to help me. Luckily, I
fix the problem finally. 

It is so simple that I just need to turn on my wireless hardware switch, which
locates on the keyboard, press F11 to turn it on. Now, I can access wireless network. 

First of all, You should use the command `sudo lshw -C network` to check the state of 
your wireless network. Then According to the output of the command, you would
know the reason why your wireless network is not available.

In addition, ubuntu documentation, [wireless troubleshooting][1] help me a lot. You 
should read it first when you meet a problem about wireless network. Hope it will help you.

[1]:https://help.ubuntu.com/10.10/internet/C/troubleshooting-wireless.html#troubleshooting-wireless-disabled 
