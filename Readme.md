# omnigollum - omniauth meets gollum

## Installation

### Manual

Clone into your ruby library path.

    git clone git://github.com/arr2036/omnigollum.git

## Configuration

Omnigollum executes an OmniAuth::Builder proc/block to figure out which providers you've configured,
then passes it on to omniauth to create the actual omniauth configuration.

To configure both omniauth and omnigollum you should add the following to your config.ru file.

### Load omnigollum library
```ruby
require 'omnigollum'
```

### Load individual provider libraries
```ruby
require 'omniauth/strategies/twitter'
require 'omniauth/strategies/open_id'
```

### Set configuration
```ruby
options = {
  # OmniAuth::Builder block is passed as a proc
  :providers => Proc.new do
    provider :twitter, 'CONSUMER_KEY', 'CONSUMER_SECRET'
    provider :open_id, OpenID::Store::Filesystem.new('/tmp')
  end,
  :dummy_auth => false
}

# :omnigollum options *must* be set before the Omnigollum extension is registered
Precious::App.set(:omnigollum, options)
```

### Register omnigollum extension with sinatra
```ruby
Precious::App.register Omnigollum::Sinatra
```

## Required patches

### mustache

Must be at v0.99.5 (currently unreleased), replace the gem version with 6c4e12d58844d99909df or
the current HEAD.

You can also (optionally) apply the patches here, to get a neat little auth
status widget in the top right corner of the page https://github.com/arr2036/gollum/commit/32de2cad920ccc6e955b8e19f6e23c2b3b4c8964



