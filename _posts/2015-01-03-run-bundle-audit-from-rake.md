---
layout: post
title: "Run bundle-audit from rake"
modified: 2015-01-03 00:07:06 -0500
tags: [programming, ruby, rake, security]
description: I want to run `bundle-audit` from a rake task in a Rails project. Here's how I did it.
---

`bundle-audit` is a command-line utility provided by the [bundler-audit ruby gem](https://github.com/rubysec/bundler-audit). It does patch-level vulnerability scans on your Ruby dependencies by working with [bundler](http://bundler.io/) to inspect your project's `Gemfile.lock`.

I want to run `bundle-audit` from a rake task in a Rails project. Here's how I did it.

This is my `lib/tasks/bundle_audit.rake` file.

~~~ruby
require 'bundler/audit/cli'

namespace :bundle_audit do
  desc 'Update bundle-audit database'
  task :update do
    Bundler::Audit::CLI.new.update
  end

  desc 'Check gems for vulns using bundle-audit'
  task :check do
    Bundler::Audit::CLI.new.check
  end

  desc 'Update vulns database and check gems using bundle-audit'
  task :run do
    Rake::Task['bundle_audit:update'].invoke
    Rake::Task['bundle_audit:check'].invoke
  end
end

task :bundle_audit do
  Rake::Task['bundle_audit:run'].invoke
end
~~~

It defines a few rasks under the `bundle_audit` namespace. Thanks to the modular Ruby code built on top of [thor](http://whatisthor.com/) I had no trouble tapping directly into the command-line implementation for `bundle-audit`.

~~~console
$ rake -T bundle_audit
rake bundle_audit:check   # Check gems for vulns using bundle-audit
rake bundle_audit:run     # Update vulns database and check gems using bundle-audit
rake bundle_audit:update  # Update bundle-audit database
~~~

Invocation is as easy as you can imagine. On the command-line:

~~~console
$ rake bundle_audit:run
Updating ruby-advisory-db ...
From https://github.com/rubysec/ruby-advisory-db
 * branch            master     -> FETCH_HEAD
Already up-to-date.
ruby-advisory-db: 108 advisories
No unpatched versions found
~~~

As you can see this does two things. First, it updates your local copy of the [ruby-advisory-db](https://github.com/rubysec/ruby-advisory-db). Then it scans your gem dependency graph looking for unpatched dependencies. What you see above is the output when everything is OK.

I also incorporated the check into my `rake test` task, because I want my tests to fail if I'm shipping with vulnerable dependencies. Here's what I have going on in `lib/tasks/test.rake`:

~~~ruby
# Remove the Rails defaults.
Rake::Task['test:all'].clear
Rake::Task['test:all:db'].clear
Rake::Task['test:db'].clear
Rake::Task['test'].clear

namespace :test do
  desc 'Run all tests'
  task all: :environment do
    Rake::Task['bundle_audit'].invoke
    Rake::Task['brakeman:run'].invoke
    Rake::Task['rubocop'].invoke
    Rake::Task['spec'].invoke
  end
end

task :test do
  Rake::Task['test:all'].invoke
end

# Running `rake` should run all my tests.
task default: :test
~~~

Since this is part of my testing expectations I can also rest easy because my continuous integration tool has my back on every change, too.
