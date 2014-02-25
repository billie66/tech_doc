### Have whenever with your rails app

* install whenever with bundler in your Gemfile

    gem 'whenever', :require => false

* Getting started

    <pre><code>$ cd /apps/my-great-project
    $ wheneverize .</code></pre>

This will create an initial config/schedule.rb file for you.

* Example schedule.rb file

  <pre><code>every 3.hours do
    runner "MyModel.some_process"
    rake "my:rake:task"
    command "/usr/bin/my_great_command"
  end</code></pre>

* The `whenever` command

  <pre><code>$ cd /apps/my-great-project
  $ whenever</code></pre>

This will simply show you your schedule.rb file converted to cron syntax. It does not read or write your crontab file.

    <pre><code>$ cd /apps/my-great-project
    $ whenever -i </code></pre>

This will write your crontab file.

    <pre><code>$ cd /apps/my-great-project
    $ whenever -s "environment=development"</code></pre>

This will set your cron jobs runnint environment. Run `whenever --help` for a complete list of options.
