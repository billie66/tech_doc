### enable wireless network in ubuntu 10.10

My laptop was Dell vostro 1088, which installed ubuntu 10.10. It was surprising
that wireless network could not work after I used it several days. I didn't know
how to handle the problem. So I thought I should reinstall the ubuntu 10.10. It
was so bad that my machine still could not connect to the wireless network and
not detect any wireless signal. Then I asked google to help me. Luckily, I
fixed the problem finally. 

It was so simple that I just needed to turn on my wireless hardware switch, which
located on the keyboard, press F11 to turn it on. Now, I could access wireless network. 

First of all, You should use the command `sudo lshw -C network` to check the state of 
your wireless network. Then According to the output of the command, you would
know the reason why your wireless network is not available.

In addition, ubuntu documentation, [wireless troubleshooting][1] helped me a lot. You 
should read it first when you meet a problem about wireless network. Hoped it will help you.

[1]:https://help.ubuntu.com/10.10/internet/C/troubleshooting-wireless.html#troubleshooting-wireless-disabled 
