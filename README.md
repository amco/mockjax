# Mockjax [![travis-ci](https://secure.travis-ci.org/ejholmes/mockjax.png)](https://secure.travis-ci.org/ejholmes/mockjax)

Mockjax gem for rails and rack applications. Define javascript mocks in your
request specs

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'mockjax'
```

## Usage
Assuming you're using capybara...

### Rack

```ruby
# spec/spec_helper.rb

Capybara.app = Rack::Build.new {
    use Rack::Mockjax
    run MyApp
}
```

#### Rails 3

```ruby
# config/initializers/test.rb

config.middleware.use Rack::Mockjax
```

Then define your stubs like you would with any other stubbing library:

```ruby
before do
  stub_ajax url: '/test', responseText: { message: 'hello world' }
end
```

Now we can make requests to `/test` from javascript and our mock will be used.
Awesome!

```coffeescript
$.getJSON '/test', (data) -> console.log(data.message) # => 'hello world'
```
