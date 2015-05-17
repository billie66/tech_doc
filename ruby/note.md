how to covert a unix timestamp to date, for example `1423888155`,

    :~$ irb
    >> Time.now.utc
    => Sat Feb 14 03:46:30 UTC 2015
    >> Time.now.utc.to_i
    => 1423885599
    >> Time.at(1423885599).utc
    => Sat Feb 14 03:46:39 UTC 2015

### check the syntax of a ruby file

    ruby -c test.rb

### encode url

escape special characters in urls

    require 'uri'
    url = 'http://site.com/big cat.png'
    puts URI.encode(url)
    => 'http://site.com/big%20cat.png'

### ruby metaprogramming

http://www.medihack.org/2011/03/15/intend-to-extend/

### check a variable or method existent

http://kakubei.blogspot.jp/2014/01/determining-whether-variable-or-method.html

### singleton

https://practicingruby.com/articles/ruby-and-the-singleton-pattern-dont-get-along

