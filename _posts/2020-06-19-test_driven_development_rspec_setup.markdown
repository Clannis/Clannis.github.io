---
layout: post
title:      "Test Driven Development (RSpec setup)"
date:       2020-06-19 05:16:38 +0000
permalink:  test_driven_development_rspec_setup
---

During my Sinatra Web Application project I found that testing every possible route and user input possibility was exausting. I would get some block of code working for a specific set of rules/tests and later have to come back to add in some other functionallity. That itself wasn't bad at all, but the fact that I had to re-test every possible edge case I wanted to account for became more and more time consuming the further into the project I got. Not only was it time consuming, it was also very repetitive. I know that during our lab assignments we work through pre-loaded spec files and decided to try and create some of my own. As far as the set up went I knew I needed a spec folder with a spec_helper file inside it. To begin, I coppied over the spec_helper file from a previous sinatra lab and wrote a simple test to see if I had set everything up correctly. Sadly, nothing worked. Since the spec_helper file first set my environment equal to 'test'

```ruby
ENV['SINATRA_ENV'] = "test"
```

getting away from the 'development' environment I had been using to build and test my project, I found I had to change my Gemfile to accomidate. I had to create a new group and load all the gems I wanted to use for testing my project through RSpec.

```ruby
group :test do
   gem "capybara", "~> 3.32" 
   gem "rspec", "~> 3.9"
   gem "rack-test", "~> 0.6.3"
   gem "database_cleaner", "~> 1.8"
end
```

Once this was working I was able to get my test to work and pass; however, there was no information that displayed that I had entered into my "describe" and "it" labels. It took quite a bit of digging and searching, but I finally found that I needed a .rspec file in my root directory. This file is used to load certain settings into rspec. Specifically for formatting in my instance. I wanted to be able to run multiple tests at once and determine which ones failed and which ones passed. My original formating displayed something along the lines of " -FF*** * ". F being failed and '*' being passed. After adding in the lines 

```
--color
--format documentation
--require spec_helper
```

to the .rspec file my output became something like

```
Homepage
   loads the homepage
	 
Sign Up
   Logged Out
	    loads the signup page (Failed -1)
```

full of color. Easily identifiable between passed and failed test and what I was testing for. (Exactly like the labs I've become so used to.)

Now with all of my set up completed, I can write tests for a specific block of code and quickly test all of my edge cases after each update to my code. Once again, sadly I decided to finally test this out towards the end of my project and wasnt able to make full use of my new found knowledge. I had manually tested everyting for my project and found I had wasted so much time in hindsight. I hope that someone new to Flatiron's Software engineering course find this blog and is able to learn from my mistake. Learn and incorporate Rspec into your projects. I promise it will save you so much time and headache. A little effort up front will be more than worth it in the end.

For those of you that want to see my full set up I have listed my full spec_helper and .rspec files below. For examples on tests just look inside a labs spec folder.

**spec_helper**
```
ENV['SINATRA_ENV'] = "test"

require_relative '../config/environment'
require 'rack/test'
require 'capybara/rspec'
require 'capybara/dsl'

if ActiveRecord::Base.connection.migration_context.needs_migration?
    raise "Migrations are pending. Run `rake db:migrate RACK_ENV=test` to resolve the issue."
end

ActiveRecord::Base.logger = nil

RSpec.configure do |config|
    config.run_all_when_everything_filtered = true
    config.filter_run :focus
    config.include Rack::Test::Methods
    config.include Capybara::DSL
    DatabaseCleaner.strategy = :truncation

    config.before do
        DatabaseCleaner.clean
    end

    config.after do
        DatabaseCleaner.clean
    end

    config.order = 'default'
end

def app 
    Rack::Builder.parse_file('config.ru').first
end

Capybara.app = app
```

**.rspec**

```
--color
--format documentation
--require spec_helper

```

