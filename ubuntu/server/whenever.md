#### Install whenever with bundler in your Gemfile

    gem 'whenever', :require => false

#### Getting started

    $ cd /apps/my-great-project
    $ wheneverize .

This will create an initial config/schedule.rb file for you.

#### Example schedule.rb file

    every 3.hours do
      runner "MyModel.some_process"
      rake "my:rake:task"
      command "/usr/bin/my_great_command"
    end

#### whenever variables

    set :environment, :development
    set :output, '/path/to/file'

#### The `whenever` command

    $ cd /apps/my-great-project
    $ whenever

This will simply show you your schedule.rb file converted to cron syntax. It does not read or write your crontab file.

    $ cd /apps/my-great-project
    $ whenever -i

This will write your crontab file.

    $ cd /apps/my-great-project
    $ whenever -s "environment=development"

This will set your cron jobs running environment. Run `whenever --help` for a complete list of options.

#### crontab command

    crontab -l      # list cron jobs created by user
    crontab -e      # edit crontab file of login user

In default, the output result of cron jobs will be sent to mailbox of login
user. The mailbox path is /var/spool/mail/username.
