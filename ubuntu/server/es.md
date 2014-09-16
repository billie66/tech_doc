*** install jdk7
    
    $ sudo apt-get install openjdk-7-jre
    $ dpkg -l | grep jdk

and make sure OS run environment is jdk7

    $ java -version
    java version "1.7.0_55"

*** install elasticsearch on ubuntu 1204

    wget https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-1.2.1.deb
    sudo dpkg -i elasticsearch-1.2.1.deb

*** start es

    sudo /etc/init.d/elasticsearch start

*** stop es

    sudo /etc/init.d/elasticsearch stop

*** make es run on bootup

    sudo update-rc.d elasticsearch defaults 95 10

*** es rake tasks

    bundle exec rake -D elasticsearch

*** es with rails example

    http://cookieshq.co.uk/posts/create-an-elastic-search-spotlight-like-search-on-rails/

*** es-analysis-ik plugin

    $ wget -O elasticsearch-analysis-ik-1.2.6.jar
    http://github.com/wyhw/elasticsearch-analysis-ik/blob/master/elasticsearch-analysis-ik-1.2.6.jar?raw=true
    --no-check-certificate

*** errors

es config file `/etc/elasticsearch/elasticsearch.yml` with
`index.analysis.analyzer.ik.type : “ik”`, access
`http://localhost:9200/index/_analyze?analyzer=ik&text=&pretty=true`

    {
      "error" : "NoShardAvailableActionException[[_na][_na] No shard available for
      [org.elasticsearch.action.admin.indices.analyze.AnalyzeRequest@7c9c15]]",
      "status" : 503
    }
