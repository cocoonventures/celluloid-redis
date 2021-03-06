Celluloid::Redis
================
[![Gem Version](https://badge.fury.io/rb/celluloid-redis.svg)](http://rubygems.org/gems/celluloid-redis)
[![MIT licensed](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/celluloid/celluloid-io/blob/master/LICENSE.txt)
[![Build Status](https://secure.travis-ci.org/celluloid/celluloid-redis.svg?branch=master)](http://travis-ci.org/celluloid/celluloid-redis)
[![Maintained: no](https://img.shields.io/maintenance/no/2016.svg)](https://github.com/celluloid/celluloid/issues/779)

A [Celluloid::IO][celluloidio]-based connection backend for the
[redis-rb][redisrb] gem, providing "evented" connection support that can
multiplex long-lived blocking calls like pub/sub and blpop(rpush) with the
Celluloid message protocol.

[celluloidio]: https://github.com/celluloid/celluloid-io
[redisrb]: https://github.com/redis/redis-rb

## Why?

Unlike EventMachine, Celluloid::IO ideally does not need to provide separate
"Celluloid-enabled" versions of each and every library that ever does any kind
of I/O, but can instead leverage dependency injection APIs that tell libraries
to use `Celluloid::IO::TCPSocket` instead of `TCPSocket`.

Unfortunately, the `redis-rb` gem is a bit gnarly and does a lot of strange
things like monkeypatching its own subclasses of `TCPSocket` and `UNIXSocket`
in attempts to add better timeout handling.

Rather than trying to inject itself into that mess, this gem provides
`Redis::Connection::Celluloid` which seeks to be a drop-in replacement for
`Redis::Connection::Ruby`.

## Installation

Add this line to your application's Gemfile:

    gem 'celluloid-redis'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install celluloid-redis

Require it in your Ruby application with:

    require 'celluloid/redis'

## Usage

When instantiating the client object, specify `:celluloid`:

```ruby
redis = Redis.new(:driver => :celluloid)
```

## Contributing

* Fork this repository on github
* Make your changes and send us a pull request
* If we like them we'll merge them
* If we've accepted a patch, feel free to ask for commit access

## License

Copyright (c) 2013 Tony Arcieri. Distributed under the MIT License. See
LICENSE.txt for further details.
