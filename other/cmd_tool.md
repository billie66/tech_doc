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

[1]: http://www.linuxtutorialblog.com/post/introduction-using-diff-and-patch-tutorial



