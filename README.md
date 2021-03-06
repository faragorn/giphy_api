# Giphy API

[![Build Status](https://travis-ci.org/faragorn/giphy_api_ruby.svg?branch=master)](https://travis-ci.org/faragorn/giphy_api_ruby)
[![codecov](https://codecov.io/gh/faragorn/giphy_api_ruby/branch/master/graph/badge.svg)](https://codecov.io/gh/faragorn/giphy_api_ruby)
[![Code Climate](https://codeclimate.com/github/faragorn/giphy_api_ruby/badges/gpa.svg)](https://codeclimate.com/github/faragorn/giphy_api_ruby)

Giphy API gem allows Ruby developers to programatically access Giphy API V1.

This gem supports all endpoints that are officially documented by Giphy. Please refer to [Giphy API Documentation](https://developers.giphy.com/docs/) for more details about endpoints and parameters.

## Installation

Add this line to your application's Gemfile:
```ruby
gem 'giphy_api_ruby'
```
or to install directly from github:
```ruby
gem 'giphy_api_ruby', github: 'faragorn/giphy_api_ruby'
```


And then execute:

    $ bundle install

## Configuration

```ruby
GiphyAPI.configure do |config|
  config.api_key = 'YOUR API KEY' # ENV['GIPHY_API_KEY'] by default
  config.json_parser = MultiJson  # JSON by default
  config.api_prefix = 'v1'        # 'v1' by default
end
```

You are highly recommended to use a different JSON parser for perfomance reasons. <br />
The easiset solution is to use [MultiJSON](https://github.com/intridea/multi_json) gem. <br />
Your custom JSON parser must implement `load` method.

## Usage

### Requesting Gifs

```ruby
# Searching Gifs by keyword:
# http://api.giphy.com/v1/gifs/search?q=aliens&api_key=YOUR_API_KEY
gifs = GiphyAPI::Gif.search('aliens')
# http://api.giphy.com/v1/gifs/search?q=aliens&limit=10&offset=20&rating=g&lang=en&api_key=YOUR_API_KEY
gifs = GiphyAPI::Gif.search('aliens', limit: 10, offset: 20, rating: 'g', lang: 'en')
#
# Trending Gifs:
# http://api.giphy.com/v1/gifs/trending?api_key=YOUR_API_KEY
gifs = GiphyAPI::Gif.trending()
# http://api.giphy.com/v1/gifs/trending?limit=20&rating=g&api_key=YOUR_API_KEY
gifs = GiphyAPI::Gif.trending(limit: 20, rating: 'g')
#
# Random Gif:
# http://api.giphy.com/v1/gifs/random?api_key=YOUR_API_KEY
gif = GiphyAPI::Gif.random()
# http://api.giphy.com/v1/gifs/random?tag=burito&rating=g&api_key=YOUR_API_KEY
gif = GiphyAPI::Gif.random(tag: 'burrito', rating: 'g')
#
# Translated Gif:
# http://api.giphy.com/v1/gifs/translate?s=moo&api_key=YOUR_API_KEY
gif = GiphyAPI::Gif.translate('moo')
#
# Get a Gif by id:
# http://api.giphy.com/v1/gifs/jWq123?api_key=YOUR_API_KEY
gif = GiphyAPI::Gif.find('jWq123')
#
# Get Gifs by a list of ids:
# http://api.giphy.com/v1/gifs?ids=jWq123,Pv01&api_key=YOUR_API_KEY
gifs = GiphyAPI::Gif.find_by_ids('jWq123', 'Pv01')
```

### Requesting Stickers
```ruby
# Searching Stickers by keyword:
# http://api.giphy.com/v1/stickers/search?q=aliens&api_key=YOUR_API_KEY
stickers = GiphyAPI::Sticker.search('aliens')
# http://api.giphy.com/v1/stickers/search?q=aliens&limit=10&offset=20&rating=g&lang=en&api_key=YOUR_API_KEY
stickers = GiphyAPI::Sticker.search('aliens', limit: 10, offset: 20, rating: 'g', lang: 'en')
#
# Trending Stickers:
# http://api.giphy.com/v1/stickers/trending?api_key=YOUR_API_KEY
stickers = GiphyAPI::Sticker.trending()
# http://api.giphy.com/v1/stickers/trending?limit=20&rating=g&api_key=YOUR_API_KEY
stickers = GiphyAPI::Sticker.trending(limit: 20, rating: 'g')
#
# Random Sticker:
# http://api.giphy.com/v1/stickers/random?api_key=YOUR_API_KEY
sticker = GiphyAPI::Sticker.random()
# http://api.giphy.com/v1/stickers/random?tag=burito&rating=g&api_key=YOUR_API_KEY
sticker = GiphyAPI::Sticker.random(tag: 'burrito', rating: 'g')
#
# Translated Sticker:
# http://api.giphy.com/v1/stickers/translate?s=moo&api_key=YOUR_API_KEY
sticker = GiphyAPI::Sticker.translate('moo')
```

### Pagination

Following pagination fields will be set to all collections if Giphy API returns a `pagination` object:

```ruby
gifs.total_count  # Total number of items available.
gifs.offset       # Position in pagination.
gifs.count        # Total number of items returned.
```

These attributes will be set to `nil` if nothing was returned.

## Development and Contributing

1. Create a fork of the original repo.
1. After checking out your fork repo, run `bundle setup` to install dependencies.
1. Create a new branch and add your changes there.
1. Commit your changes and create a pull request.

**Note:** run `rake test` to run the tests. You can also run `bundle console` for an interactive prompt that will allow you to experiment. <br />
Bug reports and pull requests are welcome on GitHub at https://github.com/faragorn/giphy_api_ruby.

## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).

## TODO List

* More tests for Base class
* Create a CLI
