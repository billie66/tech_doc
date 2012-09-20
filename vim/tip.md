#### Align a line in insert mode

    ctrl-t (forward)

    ctrl-d (backward)

#### vim paragraph reformat

If you used 'set textwidth=78', the text pasted into vim can't be aligned
automatically. The simple way to format it is to select the content, then run:

    gq 

You can check the help file for more information. Note that since _gq_ is an
operator that you can use other ways to select the text to format, but visual
mode is the most intuitive for me.

Also you could do this: 

    gq16j

The downside is that you'd have to know the line count. A more useful text
movement command to use with _gq_ is __}__, which moves you to the end of the
current paragraph. So you'd do this: 

    gq}

To format the current paragraph use: __gqap__

#### cancle the syntax highlighting of html element a 

    cp /usr/share/vim/vim73/syntax/html.vim ~/.vim/syntax/
    vim ~/.vim/syntax/html.vim

After open the file html.vim, find the following line:
    
    HtmlHiLink htmlLink                    Underlined

then use double-quote to comment the line above, which will be disabled
completely. But this don't take effect with my vim. So I replace Underlined
with italic. 


#### .vimrc 
    
    runtime vimrc
