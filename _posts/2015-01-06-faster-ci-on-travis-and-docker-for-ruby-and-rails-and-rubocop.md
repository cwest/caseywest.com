---
layout: post
title: "Faster CI on Travis (and Docker) for Ruby (and Rails (and RuboCop))"
modified: 2015-01-06 22:17:39 -0500
tags: [ruby, rails, rubocop, travis, ci]
description: I made RuboCop lose its mind.
---

If you read [my post on running bundle-audit from rake][bundle-audit] you'll also know I run [RuboCop] as part of continuous integration in [Travis CI]. Today I switched a project to run on Travis' [new docker infrastructure][travis-docker] and something hilarious happened.

# Running Travis CI on Docker

This part is super easy. Amazingly easy. Add this to your `.travis.yml` file:

~~~yaml
# Docker Infrastructure
sudo: false
cache: bundler
~~~

The `sudo` key is the magic word to build your project in a Docker container. The `cache` key will enable [bundler] caching for your project.

These two lines can speed up your build times by nearly eliminating startup costs. I went from 2.5 minutes to 24 seconds on builds which used the cache and archived images. I'm running `bundle-audit`, `brakeman`, `rubocop`, and `rspec` in 24 seconds. That is awesome!

# The funny thing is...

The first run I had a little hiccup. [RuboCop] was doing its thing and, on this project, it only has 30 files to inspect. I know that because I just ran it locally and, yep, 30 files. In the Travis environment, however, it was scanning **5320 files**. That's probably wrong.

{% pullquote %}
Turns out, {" by enabling the `cache` in Travis I caused RuboCop to lose its mind"}. How? Because of where the cache was stored. Travis put the cache in `vendor/bundle` which is in my Rails app directory and within sight of RuboCop. That's legit, but I don't actually want RuboCop to check any vendor code.
{% endpullquote %}

Why was RuboCop doing that? Because I wanted to `Exclude` a few things in my Rails app—mostly generated code—so I had a `.rubocop.yml` file that looked a little like this:

~~~yaml
require: rubocop-rspec
inherit_from: .rubocop_todo.yml
AllCops:
  Exclude:
    - 'db/schema.rb'
    - 'bin/**/*'
    - 'config/initializers/devise.rb'
    - 'config/initializers/simple_form*'
    - 'db/migrate/*'
  RunRailsCops: true
~~~

The [default RuboCop configuration][rubocop-default] _does_ exclude vendor. I need that, too, but my `Exclude` above overrides the default, so it was gone.

# The simple fix

Lets just add `vendor` back into the exclusion list:

~~~yaml
require: rubocop-rspec
inherit_from: .rubocop_todo.yml
AllCops:
  Exclude:
    - 'db/schema.rb'
    - 'bin/**/*'
    - 'config/initializers/devise.rb'
    - 'config/initializers/simple_form*'
    - 'db/migrate/*'
    - 'vendor/**/*'
  RunRailsCops: true
~~~

Voila!

Be careful when modifying RuboCop's configuration that you copy what you need to keep from the defaults, because defining an entry in your project will discard the them, not merge them.

[bundle-audit]: {% post_url 2015-01-03-run-bundle-audit-from-rake %}
[rubocop]: https://github.com/bbatsov/rubocop
[Travis CI]: https://travis-ci.org
[travis-docker]: http://blog.travis-ci.com/2014-12-17-faster-builds-with-container-based-infrastructure/
[bundler]: http://bundler.io/
[rubocop-default]: https://github.com/bbatsov/rubocop/blob/master/config/default.yml#L28
