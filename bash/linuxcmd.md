### du command 
You can use _du_ command in linux system to check the size of a file, or files 
size in a directory.    

    billie@billie-ThinkPad:/boot$ du -h
    16K ./grub/locale
    1.6M    ./grub
    121M    .

The option `-h` means printing sizes in human readable format. The above
command listed the total size of the current directory with its subdirectories 
size respectively. 

You can read man pages to get more usage of _du_. A website about the examples
of [du command][1].

[1]: http://www.labtestproject.com/linuxcmd/du_command.html

### check file type

Use _file_ command to get a file type. 

    billie@billie-ThinkPad:/$ file initrd.img
    initrd.img: symbolic link to `boot/initrd.img-2.6.35-28-generic'

### how to setup bash prompt


