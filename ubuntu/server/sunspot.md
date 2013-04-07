### full-text search with sunspot, mongoid

* Add two gems to Gemfile

    gem 'sunspot_rails'
    gem 'sunspot_mongid', :git => 'https://github.com/TV4/sunspot_mongid.git'

* bundle install

* rake sunspot:solr:start

* rake sunspot:reindex

* rake sunspot:solr:stop
