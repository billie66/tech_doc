#### how to update installed gems

    bundle update

### error

I could not find a JavaScript runtime. See sstephenson/ExecJS (GitHub) for a
list of available runtimes (ExecJS::RuntimeUnavailable).

    gem 'therubyracer'

Adding the two lines above to the Gemfile would fix the problem.

### mysql

    sudo apt-get install mysql-sever 
    sudo apt-get install libmysqlclient16-dev
    gem 'mysql2'

### check RubyGems enviroment variables

    gem env

### errors when install bundler

    billie@kitty:~$ gem install bundler
    ERROR:  Loading command: install (LoadError)
    cannot load such file -- zlib
    ERROR:  While executing gem ... (NameError)
    uninitialized constant Gem::Commands::InstallCommand
    billie@kitty:~$ sudo apt-get -y install zlib1g-dev
    billie@kitty:~$ sudo apt-get -y install libssl-dev libsqlite3-dev 
    billie@kitty:~$ sudo apt-get -y install libreadline5-dev
    billie@kitty:~$ sudo apt-get -y install curl
    billie@kitty:~$ rbenv install 1.9.3-p194
    billie@kitty:~$ rbenv rehash 

### references 

    http://docs.rubygems.org/
    rbenv wiki


