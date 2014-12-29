---
layout: post
title: "Integrated Tests Are a Scam"
description: The point of test driven development is not to do testing; it's to learn about the quality of our design.
tags: [software, design, architecture, testing]
link: http://vimeo.com/80533536
date: 2014-12-29T14:24:02-05:00
---

This is an excellent conference talk laying out the core problem with reliance on integrated tests[^integrated_tests]. I've seen this problem at several companies. Here are the steps to reproduce:

1. Build a complicated system organically.
2. Observe quality degrade.
3. Declare testing a panacea.
4. Build a large, QA-lead integrated test suite at great cost.

Now a huge, brittle test suite exists which provides no direct value to development, where it's needed most, and doesn't address the root problem: poor system design.

## Integrated test hell.

[J.B. Rainsberger](http://www.jbrains.ca/) describes the problem well. If your project has a monolithic, external test suite which relies on the entire architecture to run you are in this special hell right now. The clearest representation I can think of is his explanation of how many tests you'd have to write to get value out of an _integrated tests_ versus _isolated tests_[^isolated_tests].

A software architecture with a few interconnected components (lets say, for example: a database, REST API, UI, Job Queue) requires tests for each function of each component. If we're relying on _integrated tests_ we have to write tests to exercise every function of every component, and every combination of connections between every function of every component. As you write that software you need to write $$ O(n!) $$ integrated tests. You can't write that many tests. You don't have enough time to write enough tests to have confidence in that system. That's scary. **That's impossible.**

## The cycle.

I love this because it's clear and true. We've all seen this run-on sentence loop:

**100% of our integrated tests pass but there's a mistake[^mistake] in our software**; so we write more integrated tests to fill in the cracks which allows us to design more sloppily and gives us more opportunities for mistakes, and spending time on integrated tests means less time for isolated tests which increases the likelihood that **100% of the tests pass but we still have mistakes.**

## What should you do about this?

There is a strong correlation between large numbers of integrated tests and design problems. Integrated tests don't offer any pressure to improve our designs. Isolated tests do. Stop pretending integrated tests are helping you. Write isolated tests. 

To quote J.B.:

{% pullquote %} 
_The real benefit of isolated tests — testing one function at a time — is that those tests put tremendous pressure on our designs. Those tests are the ones that make it most clear where our design problems are. **Remember that {" the whole point of test driven development is not to do testing; it's to learn about the quality of our design "}.** We use the theory that if our design has problems then the tests will be hard to write. The tests will be hard to understand. It'll be difficult to write these small, isolated tests to check one thing at a time._
{% endpullquote %}

If you have more _isolated tests_ than _integrated tests_ chances are you have a decent design with clear interfaces and contracts between collaborating systems. This path is cheaper, faster, less likely to allow mistakes, and provides high-bandwith feedback on the quality of your software design. As you write this software you need to write $$ O(n) $$ isolated tests.

You don't have to multiply the code paths in your system to get thorough coverage, you can just add them. You go from a combinatorial explosion of tests-to-code-paths to a linear increase in tests. **That's possible.**

There's a lot of gold in this talk. Watch it. Twice!

{% vimeo 80533536 %}


[^integrated_tests]: Not to be confused with _integration tests_ (referred to in this talk as _collaboration tests_). Integrated tests require a complete, integrated architecture to run. _Integration tests_ simply test the collaboration between independent components.

[^isolated_tests]: _Isolated tests_ is a good name for tests operating on a specific function within a software architecture which exercise that function directly, in isolation, independent of any external collaborators in the architecture.

[^mistake]: Sometimes we call these defects or bugs; I agree with the speaker that's too abstract. It's a human error (more likely a series of human errors). Everywhere else in the world we call those mistakes.
