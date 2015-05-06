---
layout: post
title: "Technical Phone Screen HOWTO"
modified: 2015-04-19 16:11:53 -0400
tags: [hiring, soft skills]
description: You have 30 minutes to guess at the capability and fit of an incoming candidate. How do you do that? Here are my tips.
---

You have 30 minutes to guess at the capability and fit of an incoming candidate. How do you do that? You have to assess a few key areas quickly.

Here are my tips for the person conducting the screening, written from the perspective of the inner monologue I have when I do phone screens.

## Preparation

Skim the resume but mostly ignore it. If a recruiter was involved it's been re-arranged and re-worded to match keywords in your job posting anyway[^resume].

## Opening Questions

> On your most recent project, which areas did you focus on and contribute to, and **what did you have the most fun with?**

I'm not asking you to read your resume to me. I've seen it (and mostly ignored it). What I'm looking for here is some technical detail of your contribution. Can you articulate what you actually do? I'm technical, and you're going to be working with me all the time, so I want to hear you explain your work so I can understand it.

Even more importantly, hopefully you have enjoyed _some_ aspect of this project. Hopefully enough to tell me about it.

> **Why `$company_i_work_for`?**

I want you to have at least a passing interest in our company. If it's just, _"my recruiter told me you had an opening"_ I'm much less interested in you. Do you know what we do? Have you at least seen our website?

## Continued Education

> **How do you keep up to date with the software landscape?**

Do you read books or blogs, or subscribe to JavaScript Weekly? Do you listen to podcasts? If you don't show any interest in keeping yourself up to date this won't go well, because it means you'll allow our software to become stale, too. You don't need to be on the bleeding edge or anything, but please have read something related to your work recently.

> **What is your favorite open source project?** Anything is valid, from a library to a framework to something bigger.

This is two-fold. First, I have a bias for open source and I want to hire for that bias. I have a strong bias for building software on top of excellent pre-existing work. [Not Invented Here (NIH) syndrome](http://en.wikipedia.org/wiki/Not_invented_here) is bad news and I don't want to hire for it.

Second, something brings you joy in the work you do, right? At some point you've used a tool and been like, "This is the beset thing in the world!" For me that tool is [ponysay](https://github.com/erkin/ponysay), obviously.

## Testing

> **How do you test your current project?** Do you use BDD? Do you use CI? What's your preferred testing tool?

Even if your current project has no tests, I want to hear you be unhappy about that. I want you to know what BDD means, and CI, and use them (or want to use them). Nearly every software context has multiple testing tools to choose from. JavaScript has QUnit, Jasmine, Mocha, and others. Which one do you prefer and why? Details mean you aren't reciting the manual.

I'll be more specific on this one, because it trips up the folks who screen candidates and love testing: **it isn't the candidate's fault if their company doesn't write automated tests so don't hold that against them.**

## Technical Knowledge

> **What's your favorite feature of `$language_or_framework_you_have_used`?** What's your least favorite?

_This question can use information gained from the resume, their recent project at work, or their favorite open source project._

You should have answers to both. Something is good and something is bad, and I want to hear your opinion. Hopefully I'll even learn something new. If I disagree with you that'll be an interesting conversation for a couple minutes as we debate.

> **Have you worked with `$language_or_framework_we_are_hiring_for`?** Tell me about that.

If you've already convinced me you're a polyglot with an open, curious mind, this question isn't as critical but it's still important. I will dig into the details with you about this a bit, and explore what you've been exposed to. This is something I know well, and I'll share with you some of our real challenges in this part of the conversation.

What I'm hoping for is that when I share some of our challenges you have ideas, or questions, or both about how we're addressing them. This is particularly relevant to me, for this job, and it's your primary opportunity to convince me you can help.

## Tooling

> **What's your favorite `git` feature?**

I want you to know of git. You don't have to prefer it, but you should know of it. If you have only heard of it and had no exposure I'm sure something piqued your interest.

My favorite is the `git commit --fixup; git rebase -i --autosquash` combo. If you have used SVN I'm sure you can at least tell me better merging is something you want?

## Development Process

> **Have you worked on a software team recently? How was that?**

Working on a team is essential. Having some experience means you're more likely to fit into our culture. If you've spent the last five years in a silo it may be hard to adjust to a highly collaborative environment.

> Are you comfortable with agile software development? **What does 'agile' mean to you?**

Everyone is likely to say yes to the first question. I'm more interested in the answer to the second.

> We use code review heavily as part of the development process. **Are you comfortable with transparent, professional critique of your work?** Are you comfortable giving it, too?

This is important to us. Part of working on a team, and working with agility, is being highly collaborative and open to exploring ideas. Hesitation in response is ok, because I'm telling you we will criticize your work. However, I'm _not_ telling you we will criticize _you_. I need to know you understand the difference.

## Closing Questions

> **What do you want to do next?** Obviously you're looking for a new gig, so what is it you _want_ to be doing?

I'm looking for some kind of interest in what you do all day. Enough that you have an idea of what you'd like to be doing next. Do you want to do DevOps? Management? Become a Senior-level developer? Learn Ruby?

If you can't come up with anything then you haven't thought about it. Maybe you're going through the motions of finding a new job. Maybe you're just trying to leave a toxic, disgusting culture. That's OK. Sometimes the answer to this question is, _"I want to do the same thing I'm doing now, which I'm great at, for a new company."_

> **Do you have any questions for me?**

Please ask me something, anything. If you have zero questions you aren't really that interested in working with me. There's no way I satisfied every curiosity in this short phone call.

[^resume]: I am sad about this advice because I'm actually quite happy with [my resume](/resume/) as a piece of writing.
