### install ncurses library in ubuntu 10.10

Maybe the easy way to install ncurses is by Synaptic Package Manager, just
type libncurses in the search bar, the matching item will be shown in the
list. Then mark the required libraries for installation, then click the apply
icon, wait a while and the libraries selected will be installed.  

Actually, I didn't know which package I should choose at first, I chose
`libncursesw-dev`. After the package was installed, I compiled my programme,
the same error occurred again, the compiler couldn't find the `curses.h` file.
So I run the following commands to check if the file exists in my system.

    billie@billie-Vostro:~/Desktop/total/hen/search/curse$ sudo updatedb
    billie@billie-Vostro:~/Desktop/total/hen/search/curse$ locate libncurses.a
    billie@billie-Vostro:~/Desktop/total/hen/search/curse$ locate curses.h
    /usr/include/ncursesw/curses.h
    /usr/include/ncursesw/ncurses.h

You see, the file `curses.h` locates under the directory `ncursesw`, so
you have to use directive `#include <ncursesw/curses.h>` to tell the compiler
the exact position of the file `curses.h`. Even though I use the right `#include` 
directive, the programme can not be compiled. The below error will show. 
    
    billie@billie-Vostro:~/Desktop/total/hen/search/curse$ make
    gcc xxx.c -o xxx -g -lncurses 
    /usr/bin/ld: cannot find -lncurses
    collect2: ld returned 1 exit status
    make: *** [all] Error 1
    
Obviously, the `libncurses.a` can not be found. Why? Just simply, you can find
the answer in the above, the output of `locate libncurses.a` is empty. So, the
`libncurses.a` doesn't be installed. How to fix this problem up ? I installed
another package named `libncurses5-dev`, all problems were dealt with. 

    billie@billie-Vostro:~/Desktop/total/hen/search/curse$ sudo apt-get install libncurses5-dev 
    billie@billie-Vostro:~/Desktop/total/hen/search/curse$ sudo updatedb
    billie@billie-Vostro:~/Desktop/total/hen/search/curse$ locate curses.h
    /usr/include/curses.h
    /usr/include/ncurses.h
    /usr/include/ncursesw/curses.h
    /usr/include/ncursesw/ncurses.h
    billie@billie-Vostro:~/Desktop/total/hen/search/curse$ locate libncurses.a
    /usr/lib/libncurses.a
    billie@billie-Vostro:~/Desktop/total/hen/search/curse$ sudo dpkg -L libncurses5-dev

### 
