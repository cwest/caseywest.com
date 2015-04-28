---
layout: post
title: "There's Still No Silver Bullet (2006)"
modified: 2015-01-04 01:36:18 -0500
tags: [design, development, management, software, culture, architecture]
description: "A contemporary look on Brooks' essay No Silver Bullet: Essence and Accidents of Software Engineering"
---

> Originally published by me on [December 18, 2006](https://web.archive.org/web/20070729012936/http://blog.caseywest.com/2006/12/theres_still_no_silver_bullet_1.html) and reprinted here as-is.

[brooks]: http://en.wikipedia.org/wiki/Fred_Brooks
[essay]: http://faculty.salisbury.edu/~xswang/Research/Papers/SERelated/no-silver-bullet.pdf
[quoted]: http://www.brainyquote.com/quotes/authors/f/frederick_p_brooks_jr.html
[rails]: http://www.rubyonrails.org/
[django]: http://www.djangoproject.com/
[turbogears]: http://www.turbogears.org/
[jifty]: http://jifty.org/
[ning]: http://www.ning.com/
[productive]: https://web.archive.org/web/20070712044136/http://www.stifflog.com//2006//10//16//stiff-asks-great-programmers-answer//
[norvig]: http://norvig.com/
[dhh]: http://www.loudthinking.com/
[37signals]: http://37signals.com
[socialtext]: http://socialtext.com
[joel]: http://www.joelonsoftware.com/articles/fog0000000036.html

I recently read [Frederick P. Brooks, Jr.'s][brooks] essay [No Silver Bullet: Essence and Accidents of Software Engineering][essay]. Brooks wrote this paper 20 years ago and it still rings true today. I like the whole essay and encourage you to read it if you haven't already.

Brooks is an [oft quoted][quoted] writer. I'm going to indulge in the practice by pointing out a few things from this essay that I think will always be true.

> Likewise, a scaling-up of a software entity is not merely a repetition of the same elements in larger sizes, it is necessarily an increase in the number of different elements. In most cases, the elements interact with each other in some nonlinear fashion, and the complexity of the whole increases much more than linearly.
> 
> The complexity of software is an essential property, not an accidental one. Hence, descriptions of a software entity that abstract away its complexity often abstract away its essence.

I really like this, because today there are [a lot][rails] of [arguably excellent][django] [attempts][turbogears] to [abstract complexity][jifty] in [modern application development][ning]. Many software developers look to frameworks and application environments to manage the complexity of software development for them. These developers expect incredible gains in productivity by using a tool that makes building applications "really easy." Don't be fooled. Tools help you build things, yes, but don't expect to get a pony when you install Ruby on Rails (although, as it happens, you do get a pony when you install Jifty). Frameworks are not 100% tools, they're 80% tools. If they were 100% tools then you wouldn't be making applications you'd be writing configuration files. What kind of programmer writes configuration files for fun?

> In many cases, the software must conform because it is the most recent arrival on the scene. In others, it must conform because it is perceived as the most conformable. But in all cases, much complexity comes from conformation to other interfaces; this complexity cannot be simplified out by any redesign of the software alone.

This most obvious form of complexity through conformity in web applications is browser compatibility. I don't think that is the scenario that takes the cake, however. Anything relating to or interfacing with email clients increases complexity in an extremely non-linear fashion. There are other issues, too, such as representing information for RSS and Atom feeds. A lot of cruft exists around the edges of software because it must conform to its environment. You cannot simplify conformity within your software alone.

> In spite of progress in restricting and simplifying the structures of software, they remain inherently unvisualizable, and thus do not permit the mind to use some of its most powerful conceptual tools. This lack not only impedes the process of design within one mind, it severely hinders communication among minds.

If you've ever worked with someone else when writing software you know this to be true. The inability to visualize software is a serious friction point between team members.

When asked ["What do you think makes some programmers 10 or 100 times more productive than othes?"][productive] [Peter Norvig][norvig] answers, "The ability to fit the whole problem into their heads at one time." That's often a critical ability and it speaks to Brooks's admission that software design is hard enough within a single mind. [David Heinemeier Hansson][dhh] has a complimentary answer to the same question, "The ability to restate hard problems as easy ones." Having the ability to clearly communicate software design is important, yes. I would add to these answers, "The ability to explicitly articulate the design of complex software." Having these attributes brings you closer to making the invisible visible.

Imagine how important these skills must be if you're building a geographically distributed team like [37signals] or [Socialtext]? The lowest common denominator for being hired on these teams is likely expressed in the previous paragraph.

> I do not believe we will find productivity magic here. Program verification is a very powerful concept, and it will be very important for such things as secure operating-system kernels. The technology does not promise, however, to save labor. Verifications are so much work that only a few substantial programs have ever been verified.

20 years after writing this Brooks is still right. In context, Brooks is talking about "test first" methodologies here, asserting that testing during design and specification will not save you labor. He goes on:

> More seriously, even perfect program verification can only establish that a program meets its specification. The hardest part of the software task is arriving at a complete and consistent specification, and much of the essence of building a program is in fact the debugging of the specification.

In my opinion this statement is a key gem. I interpret this statement to be a nod to iterative development, suggesting that the imperfect art of testing our assumptions over time is a large part of the essence of software development. One could bastardize this as "release early, release often." I feel that's an oversimplification that leaves large room for error.

Taking time to design software is critical. I agree with [Joel] when he says "Programmers and software engineers who dive into code without writing a spec tend to think they're cool gunslingers, shooting from the hip. They're not. They are terribly unproductive. They write bad code and produce shoddy software, and they threaten their projects by taking giant risks which are completely uncalled for."

Let's skip to the end, to the real message within the message of the essence of software development:

> Hence, although I strongly support the technology-transfer and curriculum development efforts now under way, I think the most important single effort we can mount is to develop ways to grow great designers.
> 
> No software organization can ignore this challenge. Good managers, scarce though they be, are no scarcer than good designers. Great designers and great managers are both very rare. Most organizations spend considerable effort in finding and cultivating the management prospects; I know of none that spends equal effort in finding and developing the great designers upon whom the technical excellence of the products will ultimately depend.

This, I believe, is the most important advancement since Brooks wrote his paper. Organizations have recognized the need to grow great software designers. As a result the pace of development and product creation has increased dramatically. The state of the world is much better now than 1986 but we still have a long way to go.
