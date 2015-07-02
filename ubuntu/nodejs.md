### Installing Node.js v0.12 Debian / Ubuntu repository

    # Note the new setup script name for Node.js v0.12
    curl -sL https://deb.nodesource.com/setup_0.12 | sudo bash -

    # Then install with:
    sudo apt-get install -y nodejs

### install css-sprite to generate CSS Sprites

If you want to use css-sprite on your cli install with:

    sudo npm install -g css-sprite

Note: please wait with patience, it will take a few minutes to finish.

How to use css-sprite on your cli, run the following comand:

    css-sprite out-dir input-dir/* -s css-dir

Here you should specify image files needed, css-dir will save the
result css file named sprite.css, which can be renamed by -n option.

### npm global without sudo

### reference

* https://nodesource.com/blog/nodejs-v012-iojs-and-the-nodesource-linux-repositories

* https://github.com/sindresorhus/guides/blob/master/npm-global-without-sudo.md

