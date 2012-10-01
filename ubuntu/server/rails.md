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

    gem install bundler
    ERROR:  Loading command: install (LoadError)
    cannot load such file -- zlib
    ERROR:  While executing gem ... (NameError)
    uninitialized constant Gem::Commands::InstallCommand
    sudo apt-get -y install zlib1g-dev
    sudo apt-get -y install libssl-dev libsqlite3-dev 
    sudo apt-get -y install libreadline5-dev
    sudo apt-get -y install curl
    rbenv install 1.9.3-p194
    rbenv rehash 

### postfix

    sudo apt-get -y install postfix

send email from your application

### node.js

    sudo add-apt-repository ppa:chris-lea/node.js
    sudo apt-get update
    sudo apt-get -y install nodejs

### add a new user

    sudo adduser deployer --ingroup admin
    su deployer

### rbenv-installer (install Ruby with rbenv)

    curl -L https://raw.github.com/fesplugas/rbenv-installer/master/bin/rbenv-installer | bash

### capistrano
    
    capfile .
    cap deploy:setup
    cap deploy

### rails production env

    RAILS_ENV=production rake db:create
    RAILS_ENV=production rake db:schema:load
    RAILS_ENV=production rake db:drop
    RAILS_ENV=production rake db:drop:all
    RAILS_ENV=production rake assets:precompile 

### references 

    http://docs.rubygems.org/
    rbenv wiki


