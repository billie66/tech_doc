#### how to update installed gems

    bundle update

### error

I could not find a JavaScript runtime. See sstephenson/ExecJS (GitHub) for a
list of available runtimes (ExecJS::RuntimeUnavailable).

    gem 'therubyracer'

Adding the two lines above to the Gemfile would fix the problem.

### create a new rails project

    rails new project_name --database mysql

### create a model without test files

    rails g model Product name:string --no-test-framework

### mysql

    sudo apt-get install mysql-sever
    sudo apt-get install libmysqlclient-dev (for ubuntu 12.04)
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

* The first deployment

    capify .
    -----------------
    cap deploy:setup ( if meet errors, run `cap deploy:check` )
    ----------------
    cap deploy
    cap deploy:restart

* Subsequent deploys

    cap deploy
    cap deploy:restart

* methods

  capture <https://github.com/capistrano/capistrano/wiki/2.x-DSL-Action-Inspection-Capture>

* <http://guides.beanstalkapp.com/deployments/deploy-with-capistrano.html>

### rails production env

    RAILS_ENV=production rake db:create
    RAILS_ENV=production rake db:schema:load
    RAILS_ENV=production rake db:drop
    RAILS_ENV=production rake db:drop:all
    RAILS_ENV=production rake assets:precompile
    rails s -e production
    rails c production

### rails cache

* <http://paulbarry.com/articles/2008/04/19/serving-images-stored-in-the-database-with-rails>

* <http://www.ibm.com/developerworks/web/library/wa-rails2/index.html>

### bundle issues

* <https://github.com/carlhuda/bundler/blob/master/ISSUES.md >

### cron task

* gem 'whenever'

* whenever --update-crontab weibo //Here `weibo` is just an identifier

### Json API

* http://railscasts.com/episodes/350-rest-api-versioning?view=asciicast

* Versionist

* github json api http://developer.github.com/v3/#pagination

* rails request and response

* http header fields

### monkey patch (config/initializers)

  A monkey patch is a way to extend or modify the run-time code of dynamic
  languages without altering the original source code. This process has also
  been termed duck punching.

### rails versions

https://rubygems.org/gems/rails/versions

### rails 4 caching

http://www.slatestudio.com/blog/p/caching-in-rails-4-applications

### rake tasks

http://edelpero.svbtle.com/everything-you-always-wanted-to-know-about-writing-good-rake-tasks-but-were-afraid-to-ask
