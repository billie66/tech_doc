    face customization

    M-x list-faces-display

    install twilight

    http://github.com/crafterm/twilight-emacs

    but this requires color-theme, which used to be a ubuntu package emacs-color-themes

    but as I checked here

    http://packages.ubuntu.com/jaunty/editors/

    this package is no longer available in 9.04, must be provided by sth I do not know

    Luckily, to install color-theme is actually easy:

        * have .emacs like this

    (require 'color-theme)
    (load-file "~/.emacs.d/twilight-emacs/color-theme-twilight.el")
    (color-theme-twilight)
     

        * color-theme is here http://www.nongnu.org/color-theme/

    pet@pet-desktop:~$ tar zxvf Desktop/color-theme-6.6.0.tar.gz -C .emacs.d/
    pet@pet-desktop:~$ mv twilight-emacs/ .emacs.d/

    Note: deb available for color-theme as for 9.04

    pet@cow:~$ sudo apt-get install emacs-goodies-el

    pet@cow:~$ dpkg-query -L emacs-goodies-el|grep colo
    /usr/share/emacs/site-lisp/emacs-goodies-el/color-theme.el
    pet@cow:~$

    ctrl-c-p publish project
    face customization

    M-x list-faces-display

    install twilight

    http://github.com/crafterm/twilight-emacs

    but this requires color-theme, which used to be a ubuntu package emacs-color-themes

    but as I checked here

    http://packages.ubuntu.com/jaunty/editors/

    this package is no longer available in 9.04, must be provided by sth I do not know

    Luckily, to install color-theme is actually easy:

        * have .emacs like this

    (require 'color-theme)
    (load-file "~/.emacs.d/twilight-emacs/color-theme-twilight.el")
    (color-theme-twilight)
     

        * color-theme is here http://www.nongnu.org/color-theme/

    pet@pet-desktop:~$ tar zxvf Desktop/color-theme-6.6.0.tar.gz -C .emacs.d/
    pet@pet-desktop:~$ mv twilight-emacs/ .emacs.d/

    Note: deb available for color-theme as for 9.04

    pet@cow:~$ sudo apt-get install emacs-goodies-el

    pet@cow:~$ dpkg-query -L emacs-goodies-el|grep colo
    /usr/share/emacs/site-lisp/emacs-goodies-el/color-theme.el
    pet@cow:~$

    ctrl-c-p publish project

