---
layout: post
title: "The Mission of a DevOps Team"
tags: [press, devops]
description: The mission of a DevOps team is to eliminate itself.
image:
  feature: feature/agent-smiths.jpg
  credit: Warner Bros.
  creditlink: http://www.warnerbros.com/
---

The mission of a DevOps team is to eliminate itself.

<figure>
    <img src="/images/for-posts/devops-gears-team.jpg" alt="DevOps as a Team (DOaaT)" />
    <figcaption>
        <a href="http://blog.smartbear.com/apm/why-todays-apm-solutions-arent-optimized-for-devops/">Image source.</a>
    </figcaption>
</figure>

DevOps is a practice, not a role. It's like [agility]. _Does your company have an agile team?_ From Dave Thomas's agility redux:

> * You aren’t an agile programmer—you’re a programmer who programs with agility.
> * You don’t work on an agile team—your team exhibits agility.
> * You don’t use agile tools—you use tools that enhance your agility.

The same applies to the practice of DevOps. I suggest:

* You aren't a DevOps programmer—you're a programmer who automates deployment and operations.
* You don't work on a DevOps team—your team runs the applications you build.
* You don't use DevOps tools—you use tools that enhance your ability to ship business value.

If your company has created a dedicated "DevOps team" it signals one of two likely scenarios:

1. Things are already on fire and you're trying to catch up because you're late, or
2. You haven't realized that DevOps is a practice, like "agile", and your implementation of the concepts is likely faulty.

I do have experience building DevOps teams (responding to scenario #1, everything is on fire) and the goal of that team is always to pay the up-front investment in modernizing the software delivery pipeline. Once the investment is paid thier role is to empower engineers to run the software they create themselves, and to enable operators to avoid fires in production and get a good night's sleep. Once that equilibrium is reached it's time to move on to work which genuinely creates business value.

If your organization has a long-lived "DevOps team" and the idea is they'll always be around, how is that different from "throwing it over the wall?" In this case it's just a second wall to an intermediary team between IT and engineering, and it isn't really a good long-term strategy. It can, however, get you over the initial changes required to embrace the DevOps ideal of "you built it, you run it."

It isn't a negative that DevOps teams are created. The rational for their existence is often quite positive, just that the implementation isn't quite as polished and inline with the intent of the DevOps movement. It should be seen as a short-term tactic and you need to have a long-term strategy. Your DevOps team will never generate business value directly, so your sustained investment isn't wise.

The reduction of [cycle time](the time it takes to create and deliver business value) is, without question, a strategic advantage. Your dedicated DevOps team can get you from waterfall to agility much faster, and reduce cycle time drastically, which is a significant improvement in the short term. As the health of your architecture improves, and isn't materially affected by modification (deployment), the value gained by sustained investment in a DevOps team goes down. **This is good.**

A [recent report by Nancy Gohring of FierceDevOps](http://www.fiercedevops.com/story/newest-member-your-devops-team-may-be-someone-business/2015-07-16) suggests a new approach to solidifying the gap between engineering and IT: adding business people to its DevOps teams. (This reporting is not confirmed by Netflix, the company cited as its example.)

If you have a DevOps team their focus should be the reduction of operational costs over time, to the point where the [software deployment pipeline] is automated and the engineering and operations teams are well educated. A well automated pipeline enables engineering teams to bring their business value to customers: shipping. Educating both engineering and operations on _how_ to automate and manage your architecture empowers them to do it themselves, which distributes knowledge and reduces your [bus factor] risk.

At this point you've achieved the success of enabling and empowering _everyone_ in your product delivery organization to practice DevOps. Like the practice of agility, DevOps should be a consistent undertone as engineering delivers business value with low operational overhead.

Don't focus on operating your business. Focus on building it.

[agility]: http://pragdave.me/blog/2014/03/04/time-to-kill-agile/
[bus factor]: https://en.wikipedia.org/wiki/Bus_factor
[cycle time]: https://en.wikipedia.org/wiki/Cycle_time_variation
[software delivery pipeline]: https://en.wikipedia.org/wiki/Continuous_delivery