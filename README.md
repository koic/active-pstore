# Active PStore [![Build Status](https://travis-ci.org/koic/active-pstore.svg)](https://travis-ci.org/koic/active-pstore) [![Code Climate](https://codeclimate.com/github/koic/active-pstore/badges/gpa.svg)](https://codeclimate.com/github/koic/active-pstore) [![Gem Version](https://badge.fury.io/rb/active-pstore.svg)](http://badge.fury.io/rb/active-pstore)

This library has [Active Record](https://github.com/rails/rails/tree/master/activerecord) like interface. Use [pstore](http://docs.ruby-lang.org/en/2.2.0/PStore.html) to store data.

## FEATURES/PROBLEMS

* Oh so many problems...
* Transaction NOT supported
* Data Migration NOT supported
* Performance (caused by implementation)
* and Not solving the root cause for enterprise...

## SYNOPSIS

### class definition and instantiate

```
require 'active_pstore'

class Artist < ActivePStore::Base
  def initialize(name)
    @name = name
  end

  attr_reader :name
end

randy_rhoads = Artist.new('Randy Rhoads')
```

### specify data store path

```
Artist.establish_connection(database: '/path/to/file')
```

### save

```
randy_rhoads.save
```

database key is string of class name.

```
database = PStore.new('/path/to/file')
database.transaction {|db| artist = db['Artist'] } # fetch instances of Artist class.
```

allocate value of ActivePStore::Base#id using [SecureRandom.hex](http://ruby-doc.org/stdlib-2.2.0/libdoc/securerandom//rdoc/SecureRandom.html#method-c-hex).

```
> foo.id # => nil 
> randy_rhoads.save
> foo.id # => "0b84ece5d5be3bce3ee2101c1c4f6fda"
```

### find series

```
Artist.all
Artist.first
Artist.last
Artist.find('388980778246cbcbfcbb7a8292f28c37') # ActivePStore::Base#id is an SecureRandom.hex value
Artist.where(name: 'Randy Rhoads')
```

Range

```
Artist.where(birth_date: Date.new(1948, 12, 3)..Date.new(1956, 12, 6))
```

see spec codes for more information.

## REQUIREMENTS

no requirements

## INSTALL

Add these lines to your application's Gemfile:

```
gem 'active-pstore'
```

And then execute:

```
$ bundle
```

Or install it yourself as:

```
$ gem install active-pstore
```

## LICENCE

The MIT Licence

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
