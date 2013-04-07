### errors

Recently, I use a new laptop running ubuntu 12.04 for development my rails project. I meet
a issue when I upload image to local server.

  Errno::ENOENT (No such file or directory - identify -ping /tmp/mini_magick...

The issue above is just like this <https://github.com/jnicklas/carrierwave/issues/395>

The method to fix this problem is to install imagemagick package.

  sudo apt-get install imagemagick
