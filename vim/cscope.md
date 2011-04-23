Good tutorials about how to use Cscope to track your codebase [Cscope homepage] [1]

[1]: http://cscope.sourceforge.net/

Now, let me give you an example how to use Cscope with vim to browse through 
C source files for specified element of code. I take tig repository as an
example.
    
    billie@~/tig$ find . -name "*.[ch]" >cscope.files
    billie@~/tig$ cscope -b -k -q
    billie@~/tig$ ls | grep "cscope.*"
    cscope.files
    cscope.in.out
    cscope.out
    cscope.po.out
    billie@~/tig$ wc -l cscope.out
    35240 cscope.out

The -b flag tells Cscope to just build the database, and not launch the Cscope
GUI. The -q causes an additional, 'inverted index' file to be created, which
makes searches run much faster for large databases. Finally, -k sets Cscope's
'kernel' mode--it will not look in /usr/include for any header files that are
`#included` in your source files (this is mainly useful when you are using
Cscope with operating system and/or C library source code, as we are here). 

Of course, vim need to support Cscope, then you can run Cscope without leaving
your editor. So how can we achieve this goal? It is simple. You put a
`cscope_maps.vim` file into `$HOME/.vim/plugin` directory. After that Cscope is
combined with vim. The file can be found in Cscope official web site.


