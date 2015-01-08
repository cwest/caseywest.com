---
layout: post
title: "Responsibly Use Peek to Inspect Rails"
modified: 2015-01-07 21:51:33 -0500
tags: [ruby, rails]
description: Use these tips to keep Peek out of production.
---

I _love_ developing applications with the [peek] gem. It's designed for development or staging environments; there are a few tricks if you don't want it on production or test environments.

This gem puts a little bar on your pages which gives you all sorts of helpful information about the request you just made.

![peek screenshot]

As you can see there is information about the branch you're on, performance metrics, database queries, caches, shared memory, and job queues in there. Read the documentation for [peek] on GitHub and find the plugins that work best for you. They're excellent.

The trouble is I definitely don't want to install Peek on production, or in my test environments, and the [peek usage] instructions would, indeed, require me to do so for a few key reasons: initializers, routes, assets, and views. Using peek requires a few steps of setup in your application. Each of the areas I enumerated requires peek to be a loaded gem in the environment you're running on.

My first attempt to work around this involved wrapping calls with a [`defined?`] test. For example, in `config/routes.rb`:

~~~ruby
mount Peek::Railtie => '/peek' if defined?(Peek)
~~~

To style and script peek bar you need some CSS and JavaScript assets as well, which are loaded through the asset pipeline. Problem is, if the gem isn't in your bundle those loads fail, and so does pre-compilation if you attempt it.

Finally, your views should be checking the `peek_enabled?` method, which is defined by peek in your `ApplicationController` class. So, for example, when rendering the peek bar itself you should be doing this:

~~~haml
body
  = render 'peek/bar' if peek_enabled?
~~~

Again, if peek isn't in your Bundle, such as in the production environment, this render will fail.

I'm not particularly enthusiastic about this situation, so here is my guide to using peek responsibly. There are enough moving parts I decided to use the Table of Contents.

* Table of Contents
{:toc}

## `Gemfile`

Peek must be loaded into our environment. I'm loading it into my `:development` environment only, along with a list of Peek plugins I want to use.

~~~ruby
group :development do
  # Peek Bar
  gem 'peek'
  gem 'peek-git'
  gem 'peek-gc'
  gem 'peek-performance_bar'
  gem 'peek-pg'
end
~~~

## `PeekBar` Class

This class is meant to answer two questions:

1. _Is `Peek` available for use?_ This question is asked when we start and configure the application.
2. _Should peek be enabled for this request?_ This question is asked during requests. Specifically during view rendering for any view that incorporates peek, which is most likely a layout.

### Definition

I put this class in `lib/peek_bar.rb`.

~~~ruby
class PeekBar
  def self.available?
    !defined?(Peek).nil?
  end

  def self.enabled?(current_user)
    return false unless available?

    # The default test.
    %w(development staging).include? Rails.env
  end
end
~~~

Here you can see we've encapsulated the `defined?` test into `PeekBar.available?`. We use it in `PeekBar.enabled?` as the first test.

If peek is available, and we're in development or the `current_user` likes nerdy toys we enable peek.

### Test

I use [rspec] for testing, so my spec is in `spec/lib/peek_bar_spec.rb`.

~~~ruby
require 'rails_helper'

RSpec.describe PeekBar do
  subject { described_class }

  context 'without Peek' do
    before(:each) do
      Object.send(:remove_const, :Peek) if defined?(Peek)
    end

    it "isn't available" do
      expect(subject.available?).to be(false)
    end

    it "isn't enabled" do
      expect(subject.enabled?(anything)).to be(false)
    end
  end

  context 'with Peek' do
    before(:each) { Peek = Class.new }
    after(:each) { Object.send(:remove_const, :Peek) }

    it 'is available' do
      expect(subject.available?).to be(true)
    end

    it 'is enabled' do
      allow(Rails.env).to receive(:development?).and_return(true)
      expect(subject.enabled?(anything)).to be(true)
    end
  end
end
~~~

In order to ensure this test is isolated I take extra precautions to ensure the `Peek` constant isn't available to my tests unless I explicitly allow it.

### Initialization

By default Rails doesn't load ruby code from the `lib/` directory, so lets be sure to tell it to. In `config/application.rb` add this:

~~~ruby
config.autoload_paths += %W(
  #{config.root}/lib
)
~~~

## `PeekBarHelper` Module

As I said earlier peek implements a `peek_enabled?` method and suggests if you want to customize it define the method in your `ApplicationController` class. I recommend doing that in a helper class instead.

We need to know if peek should be enabled and to verify that we also need to know if it's available. With the `PeekBar` class this is simple.

### Definition

In `app/helpers/peek_bar_helper.rb`.

~~~ruby
module PeekBarHelper
  # Typical Peek Integration
  def peek_enabled?
    PeekBar.enabled?(current_user)
  end
end
~~~

### Test

Since we're programming responsibly here's a test for the helper. In `spec/helpers/peek_bar_helper_spec.rb`.

~~~ruby
require 'rails_helper'

RSpec.describe PeekBarHelper, type: :helper do
  before(:each) do
    allow(helper).to receive(:current_user).and_return(anything)
  end

  it 'is not enabled' do
    allow(PeekBar).to receive(:enabled?).and_return(false)
    expect(helper.peek_enabled?).to be(false)
  end

  it 'is enabled' do
    allow(PeekBar).to receive(:enabled?).and_return(true)
    expect(helper.peek_enabled?).to be(true)
  end
end
~~~

## `Peek` Initialization

The peek documentation explains how to set up `config/initializers/peek.rb` to enable the plugins you've selected. We need to first test for the availability of peek like this:

~~~ruby
if PeekBar.available?
  Peek.into Peek::Views::Git
  Peek.into Peek::Views::GC
  Peek.into Peek::Views::PerformanceBar
  Peek.into Peek::Views::PG
end
~~~

## Assets

We don't want to load or pre-compile the peek assets unless we intend to use them. My recommended approach is to wrap their inclusion in a new set of CSS and JavaScript files. I use the asset pipeline, so that's how I'll be including the gem's assets.

### CSS and JavaScript Definition

CSS is in `app/assets/stylesheets/peek_bar.scss`.

~~~css
//= require peek
//= require peek/views/performance_bar

// Peek bar on bottom of page.
#peek {
  position: fixed;
  bottom:   0;
  left:     0;
  right:    0;
  z-index:  999;
}
~~~

I prefer [CoffeeScript] so I loaded the JavaScript in `app/assets/javascripts/peek_bar.js.coffee`.

~~~coffee
#= require peek
#= require peek/views/performance_bar
~~~

### Initialization

The asset pipeline complains if you don't tell it about additional assets you intend to include separately (see the next section on [View Configuration](#view-configuration)). Thing is, we don't _always_ intend to include them or pre-compile them in this case. Just like when we initialized peek itself we must check for its availability.

Add this to `config/initializers/assets.rb`:

~~~ruby
if PeekBar.available?
  Rails.application.config.assets.precompile += %w(peek_bar.css peek_bar.js)
end
~~~

### Default Assets Gotcha

By default `application.css` and `application.js` include all the CSS and JavaScript in their respective directory trees. That's achieved through the use of `require_tree .` in each of those files.

Now that we've created a couple assets to conditionally load we need to remove `require_tree`. If you don't remove it your default assets will try to include `peek_bar.*` which will lead to the aforementioned failures on environments where peek is not installed.

If you were relying on it, which I don't recommend for reasons beyond the scope of this essay, learn how to deal with it by reading the [Asset Pipeline Rails Guide][asset-pipeline].

## View Configuration

All this hard work for what? Now it's time to tie it all together in our layout view. I like [slim] so this is an extremely condensed version of my default layout, `app/views/layouts/application.html.slim`.

~~~haml
doctype html
html
  head
    = stylesheet_link_tag 'application', media: 'all', 'data-turbolinks-track' => true
    - if peek_enabled?
      = stylesheet_link_tag 'peek_bar', media: 'all', 'data-turbolinks-track' => true
    = csrf_meta_tags
body
  = render 'peek/bar' if peek_enabled?
  = yield
  = javascript_include_tag 'application', 'data-turbolinks-track' => true
  - if peek_enabled?
    = javascript_include_tag 'peek_bar', 'data-turbolinks-track' => true
~~~

## Finally

Voila!

At this point [peek] is incorporated into my application in a robust, responsible way. Environments we didn't install it into operate perfectly without it, and the ones we do have an encapsulation to use for managing its inclusion in our interface.

It was a little more work but it paid off. We have an excellent developer tool installed without hurting production.

If we want to use peek in production with only staff accounts, for example, all we have to do is change the `Gemfile` to install peek in the `:production` group and adjust the `PeekBar.enabled?` method:

~~~ruby
def self.enabled?(current_user)
  return false unless available?

  Rails.env.development? || current_user.staff?
end
~~~

That `PeekBar` class really tied the room together, did it not?

{% youtube ezQLP1dj_t8 %}

[peek]: https://github.com/peek/peek
[peek screenshot]: https://f.cloud.github.com/assets/79995/244991/03cee1fa-8a74-11e2-8e33-283cf1298a60.png
[peek usage]: https://github.com/peek/peek/blob/master/README.md#usage
[`defined?`]: http://ruby-doc.org/docs/keywords/1.9/Object.html#method-i-defined-3F
[rspec]: https://relishapp.com/rspec/rspec-rails/docs
[asset-pipeline]: http://guides.rubyonrails.org/asset_pipeline.html#manifest-files-and-directives
[CoffeeScript]: http://coffeescript.org/
[slim]: http://slim-lang.com/
