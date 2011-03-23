This article was about how to light a LED on s3c2410 board.
The whole process was as the following. This was composed of four stages.

### Firstly burn _vivi_ to test board

I thought this should be easy and I would finish the job quickly because I 
had done it before. Actually I was wrong, I even didn't know how to take the 
first step. Sadly, I forgot all the steps needed to light the LED. At the moment 
I realized the importance of taking notes.

Prepared the _vivi_, opened the _hyperterminal_ in Windows _xp_ OS and set all 
parameters according to the port you are using. I used _com2_, _bps_ was `115200`, 
the control of data streams was `none`. Connected the serial port of the test 
board and usb power supply.

Additionally you must have a burning-tool called _JTAG_. Connected one end of 
_JTAG_ to your 25 pins parallel port, the other end to the test board.

Now you still couldn't do anything. Must install parallel _GIVEIO_ driver in _xp_.

1. put the GIVEIO driver into `c:\WINDOWS\system32\drivers\`
2. open `adding hardware wizard`,
3. click `the next step`,
4. select `yes,i have linked this hardware` and click `the next step`,
5. select `adding new hardware device` and click `the next step`,
6. select `install manually selecting from the list(advance)`and select `display all devices`,
7. select "install from the disk"and click "look into"
8. select installation inf file(.inf)

Run _cmd_ application. Executed `JTAG software-burning sjf2410wiggler` command.
Before you run the command, you should put _vivi_ and _sjf2410wiggler_ 
in the same directory `c:\`. Then executed `sjf2410wiggler /f:vivi`, then 
run `SEC JTAG FLASH<SJF>`. You needed to type the proper number in the term of the prompt.

1. select the function to test:0 K9S1200 prog  (test flash) NAND Flash
2. as above:0 K9S1200 program                  (prepare to burn)
3. target start block number:0                  burning
4. :2  exit

OK, the _vivi_ was burned into test board, you can continue. 

### Secondly load the kernel zimage into the test board

When I had done the first step, I tried to load kernel.

1. Install `sec soc usb bluk` slave driver in _xp_ as installing _GIVEIO_, 
unluckily I can't install it `no installtion inf about the driver, 
the fact is that it is the .inf file`.
2. Click the space key, then power on, boot the _vivi_, display _vivi_.
3. Link usb wire to the usb slave port in board.
4. Boot _DNW_ but I can't see `usb:ok`.

Tried again and again, but I didn't succeed. I couldn't settle this problem, 
so I asked peter for help. In the beginning, peter did the same thing 
as me and the problem appeared again. When he booted the _vivi_, he found 
the _vivi_ didn't have `loadyaffs` command, so he told me that 
the _vivi_ didn't support usb slave that meant no usb slave driver in the _vivi_.
DIY was very important. 

1. Reburn a _vivi_ into the test board which support usb download
2. Boot the _vivi_ and link usb wire and enter `load flash kernel u`
3. Boot DNW appearing `usb:ok configuration/option(bps-115200,port-com2) "usb port"/transmit/`
   (select kernel zimage)
4. pull the usb wire when this is done

### Thirdly load root filesystem by usb port

1. Reboot the _vivi_, link usb wire, enter `loadyaffs -e root u`

2. Reboot _DNW_ and do as loading kernel

Before you loaded the root filesystem, you should use _mkyaffsimage_ tool to
make _.yaffs_ image file of root filesystem. Added `/etc/pointercal` file to the
root filesystem, otherwise you could not boot OS when all work were done. Used
command `mkyaffsimage <directory name> <filename.yaffs>` to finish the job.
When this was done, the OS in the test board had been built.

### Fourthly load applications

Write LED driver
