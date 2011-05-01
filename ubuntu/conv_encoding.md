
### convert the encoding method of a given file  

When open a file, maybe you see the file messed up with a lot of odd symbols. This means
your system wide locale native encoding don't support the encoding of the file. So using `iconv` command, 
convert encoding of given files from one encoding to another. For example, there is a file written
in traditional Chinese encoded by `big5` character sets. But I can't view this file. Then
I need to covert the encoding of this file from `big5` to `utf8`.

    iconv -f big5 -t utf8 oldfile -o newfile

If covert a file from traditional utf8 encoding to simplified utf8 encoding,
which is a little complex.

    iconv -f utf8 -t big5 oldfile | iconv -f big5 -t gb2312 | iconv -f gb2312 -t utf8 -o newfile 

So, first you should figure out what a file encoding type is, you can use the
following command.
    
    file -bi filename

There are also two utilities can convert the encoding of a file, `recode` and
`enconv`. They are not installed in ubuntu 10.10 by default. So you should
install them first. The `recode` will rewrite the original file with the
locale native encoding automatically, the old file will disappear.

    recode big5 oldfile 

### locale in ubuntu

List all the available locales in your system, use `locale -a`. You can go to
directory `/usr/share/locales` to install specified language package.Then run
`dpkg-reconfigure locales`. 
