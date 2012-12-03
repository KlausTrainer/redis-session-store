A simple Redis-based session store for Redis. But why, you ask,
when there's [redis-store](http://github.com/jodosha/redis-store/)?
redis-store is a one-fits-all solution, and I found it not to work
properly with Rails, mostly due to a problem that seemed to lie in
Rack's Abstract::ID class. I wanted something that worked, so I
blatantly stole the code from Rails' MemCacheStore and turned it
into a Redis version. No support for fancy stuff like distributed
storage across several Redis instances. Feel free to add what you
seem fit.

This library doesn't offer anything related to caching, and is
only suitable for Rails applications. For other frameworks or
drop-in support for caching, check out
[redis-store](http://github.com/jodosha/redis-store/)

Installation
============

    gem install redis-session-store

Configuration
=============

In your Rails app, throw in an initializer according to the following example:

    options = {
      :db => 2,
      :expire_after => 120.minutes,
      :key_prefix => "myapp:session:"
    }
    MyApp::Application.config.session_store :redis_session_store, options

See lib/redis-session-store.rb for a list of valid options.

Changes
=======

* Use setex for a single command instead of sending two commands. (Thanks dplummer)
