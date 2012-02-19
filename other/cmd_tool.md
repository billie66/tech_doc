unpack a .rar archive 

    apt-get install unrar

unpack on current directory

    unrar e

A good tutorial about diff and patch commands, [diff and patch][1]

ssh command

    ssh -t USER,PROJECT@shell.sourceforge.net create

Note that you can access remote shell through this operation.The detail about 
ssh will be covered next time.

    ssh -t billie66,tinylion@shell.sourceforge.net create

rsync command

    rsync -r --delete local_file_directory/ billie66@frs.sourceforge.net:/home/users/b/bi/billie66/userweb/htdocs/

Note that "/" is very important

    rsync -r /var/www/ billie66@frs.sourceforge.net:/home/users/b/bi/billie66/userweb/htdocs/

check file's size

    du -m/-sh filename

make root filesystem

    mkyaffsimage root root.yaffs

remove installed package with configration files( a complete removal of package )

    apt-get --purge remove packagename

get many details about the package that you want (or don't want)to install

    apt-cache show package

The output include the information of the package which has been installed in your system.

check file's type

    file filename

dd command

To make an ISO from your CD/DVD, place the media in your drive but do not
mount it. If it automounts, unmount it. 

    dd if=/dev/dvd of=dvd.iso # for dvd 
    dd if=/dev/cdrom of=cd.iso # for cdrom 
    dd if=/dev/scd0 of=cd.iso # if cdrom is scsi 

To make an ISO from files on your hard drive, create a directory which holds
the files you want. Then use the mkisofs command. 

    mkisofs -o /tmp/cd.iso /tmp/directory/ 

This results in a file called cd.iso in folder /tmp which contains all the
files and directories in /tmp/directory/. 

[1]: http://www.linuxtutorialblog.com/post/introduction-using-diff-and-patch-tutorial



