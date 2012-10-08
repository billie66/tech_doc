### What is memcache?

---
Memcache is a system that works to speed up servers by caching server
information. The program allows you to allocate a specific amount of the
server ram toward caching recently queried data for a certain amount of time.
Once the data is requested again, memcache speeds up the process of retrieving
it by displaying the cached information instead of generating the result from
the database. 
---

### Install memcache

    sudo apt-get update
    sudo apt-get install memcached

### combine with rails

    gem install dalli

### Great articles

* <https://docs.djangoproject.com/en/1.4/topics/cache/>

* <https://github.com/mperham/dalli/issues/106>
