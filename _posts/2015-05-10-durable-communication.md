---
layout: post
title: "Durable Communication"
modified: 2015-05-10 18:32:22 -0400
tags: [soft skills, remote work, leadership, communication]
description: It's not inherently harder to be a tech lead while remote or on a distributed team – it's more deliberate.
---

It's not inherently harder to be a tech lead while remote or on a distributed team – it's more deliberate.

I [tweeted] this sentiment recently along with the concept of _durable communication_. That phrase is inspired by data storage which is typically grouped into two categories: durable and ephemeral. I often hear people say it's harder to work remotely, and very hard to be in a leadership position remotely. It's said as common sense, an obvious truth. I think that's a cop out. I don't buy it for a second.

_**Before we continue:** This post is about being a remote worker or working on a distributed team. I am convinced this is the path software organizations are rightly headed, and I'm determined to help you get there. If your organization has no remote workers, by choice or otherwise, or if you think remote work or remote leadership is out of the question this post may not be for you. That's cool. On the other hand, maybe it'll give you the tools, vocabulary, and confidence to give it a shot. Either way I look forward to hearing about it._

<!-- MarkdownTOC -->

- [What is Durable Communication?](#what-is-durable-communication)
- [Why do I care?](#why-do-i-care)
- [Effective Communication Saves Time](#effective-communication-saves-time)
- [Transparent by Default](#transparent-by-default)
- [Shared Responsibility](#shared-responsibility)
- [Change _is_ Hard](#change-_is_-hard)
- [Tools](#tools)
    - [Text Chat](#text-chat)
        - [ChatOps](#chatops)
    - [Audio/Video Communication](#audiovideo-communication)
    - [Screen Sharing](#screen-sharing)
    - [Development Tools](#development-tools)
        - [Commit Messages](#commit-messages)
        - [Code Review](#code-review)
        - [Digital Agile Board](#digital-agile-board)
    - [Collaborative Writing](#collaborative-writing)
    - [File Store](#file-store)
    - [Shared Calendar](#shared-calendar)
    - [Email](#email)
- [Techniques](#techniques)
    - [Everyone Should Experience Remote](#everyone-should-experience-remote)
    - [Face Time (Onsite)](#face-time-onsite)
    - [Invite Remotes to Hallway Conversation](#invite-remotes-to-hallway-conversation)
    - [Over Communicate](#over-communicate)
        - [Share Your Personality (Off Topic)](#share-your-personality-off-topic)
        - [Have a Visible Pulse](#have-a-visible-pulse)
    - [Pick a Timezone](#pick-a-timezone)
- [Conway's Law](#conways-law)

<!-- /MarkdownTOC -->

# What is Durable Communication?

Collaboration using deliberately inclusive, transparent, and reliable tools and techniques. It's the cornerstone of successful remote work.

# Why do I care?

I currently lead three teams in a distributed engineering organization. One is entirely based in California, another entirely in Pennsylvania, and the third is split between those locations. If I'm going to be successful it's critical to me, and to my teams, that we get communication right. I admit to being a change agent and this is one of the ways I've changed the engineering organization. This essay describes how my teams communicate.

# Effective Communication Saves Time

Communication is more deliberate, it's more intentional, when you're remote and communicating effectively. In a distributed team where pockets of people are co-located it's easy to unintentionally make decisions and share facts. It happens in the kitchen or at lunch. When communicating with someone far away from you, physically, you have to choose to share. It's not an accident.

If you want to succeed at remote work it requires deliberate changes to the way your team communicates. It's a conscious choice to alter behaviors and culture to better suit a distributed group of people.

This is a skill which can be acquired. It takes practice. Here's the thing: it's no more effort than accidental communication and, in fact, it saves everyone time and energy in the long run when information is freely flowing in channels designed to share broadly.

Over time it becomes more comfortable to communicate in a shared space and you'll soon find yourself choosing that by default. You'll say, _"I just learned something weird about our data schema. I'll tell you in our chat room."_ As you describe the oddity that is your data model, in the chat room, you're sharing with everyone regardless of physical location.

# Transparent by Default

One of the most striking changes a team experiences when practicing durable communication is the substantial increase in their transparency. Most communication is in the open. It's archived and indexed. Anyone can read it.

It's like giving your team the super power of time travel. In three years someone is going to be asking, _"Why the hell did we define an enum for this obviously boolean attribute and by the way querying it is timing out on large data sets?!"_ They're going to search your chat archives, read commit history, find tickets, and learn that the attribute was supposed to have five values and was simplified three days before launch because otherwise we weren't going to finish[^yagni].

Thank your lucky stars! All the engineers who worked on that feature have moved on to new opportunities and there's nobody left to ask in the hallway. Good thing your communication was durable. Always err on the side of transparency. It'll save your future ass.

# Shared Responsibility

Responsibility for durable communication is shared among everyone in a distributed organization; everyone is accountable for their part in making collaboration maximally effective.

Your organization
: has a responsibility to provide a collection of tools to enable distributed collaboration.

Your team
: has a collective responsibility to cultivate a culture built on the techniques of durable communication.

You
: have a responsibility to provide continual feedback when communication is becoming ineffective.
: &nbsp;
: This may be during a conference call when two people are having a side conversation and suddenly you can't follow anything being said. _"Excuse me, I can't follow multiple conversations at once. Can we do one at a time?"_
: &nbsp;
: It may be during a retrospective to highlight key decisions made beyond your visibility. _"I was surprised to learn we decided on Elixir for the spike. If it was written down I didn't see it."_

# Change _is_ Hard

If your organization is expanding from co-located to distributed it will come with growing pains. Once durable communication has been fully embraced it will feel effortless. Transition won't feel that way, and that's okay. Change requires additional effort and _that_ is hard, but it's effort spent going in the right direction so it's well spent.

What follows are concrete methods for reducing the pain of distributed work. It's tailored for teams building software.

# Tools

I'm going to list a handful of options ranging from completely free to paid. These are things I know about. They aren't endorsements unless explicitly stated. In other words, you should do the cost/benefit analysis for your organization and choose wisely.

## Text Chat

This is the primary device for durable communication. In my experience it's the most critical tool in your collaboration toolbox. There are some specific features which make it invaluable, and any deployment should have them one way or another:

Archive
: An indexed, searchable archive is particularly important. This is a history of your teams' informal communication and, just like in the hallway, a ton of knowledge sharing and key decisions are made here. You want to remember that.

Group Chat
: It's not enough to have one-on-one chat capability, however…

Private Chat
: it's also important for individuals to be able to communicate.

Full Participation
: Everyone in your organization should be able to use it, and should be using it.

Try [HipChat], [Slack], [IRC], [Google Hangouts], or [jabber].

### ChatOps

[ChatOps] is the use of text chat tools for the transparent automation of business practices. It's so awesome it has a heading. Typically ChatOps is achieved by deploying a bot, which connects to your chat system, and can be programmed to do tasks for you. For example, it could build a new release, do a full deployment, pick a place for lunch, or find the perfect animated GIF for the conversation. It's  fun and useful!

ChatOps also helps introduce context into your conversations. It can be hard to know what's going on when you're on a distributed team and we can bridge that gap by doing some of that work right in a chat room where everyone can see it. No more wondering when a release is happening. You just saw someone start a release, and you just saw your bot report the release happened successfully.

Try [hubot] or [Lita]. [HipChat] and [Slack] also have a lot of built-in integrations with external services to provide the reporting aspects of ChatOps out of the box.

More on ChatOps: [Carol Nichols], ["How is ChatOps Formed?"](http://slides.com/carolnichols/chatops#/) ([video](https://www.youtube.com/watch?v=BX-iT5xBaMY)).

## Audio/Video Communication

Everyone should be able to have a phone call, or Internet equivalent, when they're at work. Voice is fine, usually, and video is higher bandwidth. Non-verbal communication is a huge part of human communication and it should absolutely be a part of your remote work environment. (Please don't make the joke about not wearing pants. It's not funny anymore.)

This tool requires some hardware. It's necessary equipment to effectively do your job and your company should provide it or reimburse you for reasonable expenses.

Headphones
: Yes, you need headphones. Unless you're sharing audio with a room you should be waring headphones on a call or video chat. If you don't you run the risk of an audio feedback loop. Software is still spotty at avoiding this.
: &nbsp;
: The other reason for headphones is if you're working on a distributed team with pockets of co-located people there's a likelihood you'll end up on the same call as several people around you. There's nothing worse than hearing someone speak twice, on a slight delay, so it sounds like an echo. Oh, there is something worse: hearing _yourself_ when you're talking, on a slight delay.

Microphone
: I recommend getting a set of headphones with a built-in microphone. A lot of the reasons for having one are the same as above.
: &nbsp;
: The times when this breaks down are meetings where most people are co-located and a lot of them are speaking. An example is standup with a couple remote workers and everyone else physically gathered. For these cases I recommend a microphone which can be passed around when someone is speaking. This serves two purposes: high quality audio for the speaker regardless of their location in the room, and it tends to force the group to speak one at a time.

Camera
: Most laptops and all-in-one desktops come with cameras these days and they're usually good enough for these purposes.
: &nbsp;
: The times when this breaks down is conference room meetings, often with whiteboards, where a small number of participants are remote. If your company is fancy they can buy great solutions for this problem. A cheap option is an external camera which someone in the meeting can pan and zoom for you. Cheap and effective.

There are three important features of any effective audio/video communication tool: the ability to have one-on-one calls, the ability to conduct group conference calls, and the ability to do either in 60 seconds or less. This collection of features isn't always available in a single tool, and that's okay. Use a few if you have to. It'll pay off.

Try [HipChat] \(one on one), [Skype], [Webex], [talky], [sqwiggle], or [Google Hangouts].

## Screen Sharing

This is your fast-track to remote pair programming, troubleshooting, hallway testing, and collaborating with other disciplines. The important features are the same as for audio/video calls: one-on-one sharing, group sharing, and the ability to do either in 60 seconds or less.


Try [Screenhero] \(for [Slack]), [HipChat], [join.me], or [Webex].

## Development Tools

### Commit Messages

> "The only difference between science and screwing around is writing it down." – [Adam Savage], Mythbusters

Commits are like emails to future developers. Please write good commit messages for our _future_ selves. 
And not just ourselves, but any future developers working on this code. 

_Think of it as time travel_. When [Marty wrote Doc that letter](http://backtothefuture.wikia.com/wiki/Marty%27s_letter), it wasn’t a cryptic, 
short message he would only understand in-context. It wasn't simply a P.O. Box address for Doc to go find the details at. It was a clear description of the problem and solution. It was helpful as soon as it was read.

_Commits are always in sync with the code_. This is awesome. 
It means we can write documentation about our code without the worry of it getting stale. 
That's better than comments, even. A commit message for a piece of code lasts exactly as 
long as the code it's talking about lasts.

More on commit messages:

* Alex 'Skud' Bayley, ["Start Your Commit Message with a Verb"](http://infotrope.net/2013/08/24/start-your-commit-message-with-a-verb/)
* Stephen Ball, ["Deliberate Git"](http://rakeroutes.com/blog/deliberate-git/) ([video](https://vimeo.com/72762735))

### Code Review

Written, asynchronous code review is a central part of any solid development cycle. Don't take my word for it. From the excellent book, [Code Complete](http://www.amazon.com/Code-Complete-Practical-Handbook-Construction/dp/0735619670):

> …software testing alone has limited effectiveness -- the average defect detection rate is only 25 percent for unit testing, 35 percent for function testing, and 45 percent for integration testing. In contrast, **the average effectiveness of design and code inspections are 55 and 60 percent.** Case studies of review results have been impressive:
>
> * In a software-maintenance organization, 55 percent of one-line maintenance changes were in error before code reviews were introduced. After reviews were introduced, only 2 percent of the changes were in error. When all changes were considered, 95 percent were correct the first time after reviews were introduced. Before reviews were introduced, under 20 percent were correct the first time.
> * In a group of 11 programs developed by the same group of people, the first 5 were developed without reviews. The remaining 6 were developed with reviews. After all the programs were released to production, the first 5 had an average of 4.5 errors per 100 lines of code. The 6 that had been inspected had an average of only 0.82 errors per 100. Reviews cut the errors by over 80 percent.
> * The Aetna Insurance Company found 82 percent of the errors in a program by using inspections and was able to decrease its development resources by 20 percent.
> * IBM's 500,000 line Orbit project used 11 levels of inspections. It was delivered early and had only about 1 percent of the errors that would normally be expected.
> * A study of an organization at AT&T with more than 200 people reported a 14 percent increase in productivity and a 90 percent decrease in defects after the organization introduced reviews.
> * Jet Propulsion Laboratories estimates that it saves about $25,000 per inspection by finding and fixing defects at an early stage.

Copied from [Coding Horror's copy](http://blog.codinghorror.com/code-reviews-just-do-it/).

Yes, you still need to write tests. Automated testing is not enough to find defects early. Combining them with code review is a winning strategy. Code review reduces defects, increases learning and knowledge sharing, and serves as a written artifact of technical decisions made over time.

Some options for deploying code reviews include [GitHub Pull Requests], [Gerrit], [ReviewBoard], [Code Collaborator]

### Digital Agile Board

Sticky notes don't scale. I'll caution you here: this is not an opportunity to over-architect your development process. You need a few queues to understand the workload of each step in your development pipeline. This gives you insight into capacity and constraints, and provides a high-level picture of work in progress.

Try [Trello], [Pivotal Tracker], [JIRA's Agile Plugin], [Waffle], or [GitHub Issues].

## Collaborative Writing

Being able to take notes together in meetings is very powerful. A real-time document sharing tool brings people together in meetings and serves as a very powerful alternative to a whiteboard. Someone can decide to take live notes while others cleanup structure and edit behind them. Everyone can see the conversational history and it can be preserved for posterity.

Try [Etherpad], [Hackpad], [Google Docs], [GitHub Wiki], or [Confluence].

## File Store

Sharing large files is hard, still. Especially at work. It might be PSDs, PDFs, or OVAs. Making this easier will ease a common pain point of distributed teams. The solution you choose will depend on your particular risk profile.

Try [Dropbox], [Box], [NFS], [WebDAV], or [Google Drive].

## Shared Calendar

Availability must be constantly communicated. Picking a time to get people together across locations and timezones can be a challenge. Shared calendars solve that problem. Frankly, I wish there were more options here. If you know of any solid alternatives I'd love to hear about them.

Try [Exchange] or [Google Calendar].

## Email

No, not really. Email is often one of the slowest, least effective means of collaboration and I don't recommend relying on it for that purpose. It does have a place, and I feel that place is in non-critical communication with no time pressure. For example, when you want to chat with someone who isn't "in the office" at that particular moment and it's not important enough to call them.

It's also an effective way to receive reports and notifications which, often, will lead you to the other collaboration tools mentioned in this document.

If you need a quick answer from a co-worker or team and you're starting to write an email I have this advice: **stop.** You're about to waste time and introduce needless delay. I bet you'll get a faster answer on text chat.

# Techniques

## Everyone Should Experience Remote

At some point you should send every team member home, or to their local coffee shop, or into separated conference rooms to simulate being remote. Empathy is a great motivator, and if the folks at headquarters are having trouble adjusting to your remote workforce this is a fast-track way to help.

I love the idea of having everyone work from home (or wherever) every Friday. A policy like this tends to make people happy. They like it. However, it's not a big enough burden to change minds most of the time. It'll become your "heads down day" and the point of the exercise will be lost.

I recommend at least a full week. Everyone is remote. Meetings continue as scheduled. So do pair programming and planning sessions. Standup? Yes. Meetings with other departments? Yes, plan to dial in or video conference.

There's a higher-level business benefit to doing this regularly, too. It can serve as a good, real test of your operational business continuity plans. It's a sustained use of the tools you've put in place for when your office burns to the ground. You are thinking about how to operate the company when your office is on fire, right?

There are team members for whom home is not a suitable work environment. Speaking as a dad who had toddlers I can tell you sometimes it just isn't going to be viable. Don't require everyone to be at home. For folks who can't they should be offered the option of renting a desk at a co-working space (to be expensed), or commandeering a conference room for the week. If they stay in the office, in a conference room, set a rule of no talking in person. Stay true to the simulation.

## Face Time (Onsite)

Get people together. Relationships are best created in person and can be sustained remotely for a while. Minimum twice a year. Being together is too valuable to waste on business as usual. Close the laptops and get to know each other for a while.

## Invite Remotes to Hallway Conversation

It is inevitable, and still good and healthy, that you'll strike up an ad hoc conversation at your desk. It'll probably be about work, and chances are someone in another location is interested in that topic. This is a moment to invite them in. How do you do that when they're in another timezone? A few ways.

Invite them on video chat. This is the best. It's like you're right there in the room because your head is! Unplug your headphones so they can hear everyone and everyone can hear them. You can also invite them to audio, or you can all hop on chat and have the conversation in text. Video is still the highest bandwidth option and for that reason I recommend it.

If you work in an open office you're probably saying something I hear all the time, _"but we'll need to find a conference room because it's rude to be on a call in the pit."_ No, it's not. It's no more rude than the conversation you're having right now. Will it surprise people? Yes, at first. They'll get over it. This is a stigma that should be eliminated. It's also what headphones were invented for.

## Over Communicate

Your working relationships will benefit from the old adage "always over-communicate", just like any relationship.

### Share Your Personality (Off Topic)

A benefit to being co-located with your peers is they get to know you. They learn about your kids, your hobbies, and your affinity for mango flavored tea. Even if you never said anything about it out loud they'd learn about you just from being nearby.

Remote co-workers don't have the luxury of osmosis. Our relationships grow over time through familiarity and comfort. The more we know someone the closer we feel. That's why it's important to share your personality. Share it a lot. How? Off topic.

Every organization needs an Off Topic chat room. This is where the stream of nonsense we all spew every day goes to live. This is where you tell someone you're getting coffee, where you post pictures from last weekend's mountain biking adventure, or where you drop a link to the latest badass thing [Neil deGrasse Tyson] just said. Off Topic is a safe place to chat about whatever you want with your co-workers.

You may end up with more off topic channels, for specific interests, than work-specific channels. That's ok! I see channels for music, cooking, exercise, and DIY often. Let this thrive and grow organically.

For those of you who lead remote or distributed organizations: (with the exception of offensive content) don't monitor or question the traffic in this room. There will probably be a lot of it, and if you've forgotten what it's like to build a thing you'll probably also wonder how these people get anything done all day. Don't worry about it. This is work. Instead of hearing it in the halls you're seeing it on the screen. No big deal.

### Have a Visible Pulse

When you're remote it's your responsibility to exhibit a visible pulse. You may think nobody cares about every time you make a pot of coffee or push a branch, and you're probably right about that. What they do care about is knowing you're alive, there, and available when needed. Sending those seemingly useless messages is sending them a more important signal: you are reliable and okay.

## Pick a Timezone

Your company probably has a home office. It can be helpful to agree that its timezone is your _Standard Operating Time (SOT)_. I've employed this technique before and it works.

When is standup every day? _10am SOT_

_I'll be leaving the office a little early today so reach be before 1PM SOT if you need anything._

When discussing time you should always be explicit about timezones. The _Standard Operating Time_ technique provides an generalized solution. Each individual can translate SOT to their native timezone. After a little practice it'll be second nature.

# Conway's Law

Durable communication exhibits the same characteristics as accidental, convenient communication in a co-located space. The powerful difference is how inclusive, transparent, and reliable it is. Durable communication tools and techniques not only scale well with your organization, they'll empower your organization scale well, too.

[Conway's law] states that _"organizations which design systems ... are constrained to produce designs which are copies of the communication structures of these organizations"_.

The health and quality of your product will be a direct reflection of the health and quality of your organization. Take great care of your organization and it will pay off in your product.

[Conway's Law]: https://en.wikipedia.org/wiki/Conway%27s_Law
[tweeted]: https://twitter.com/caseywest/status/597027263796912128
[YAGNI]: https://en.wikipedia.org/wiki/YAGNI
[Neil deGrasse Tyson]: https://twitter.com/neiltyson
[HipChat]: https://www.hipchat.com/
[Slack]: https://slack.com/
[Screenhero]: https://screenhero.com/
[IRC]: http://www.irc.org/
[jabber]: http://www.jabber.org/
[Google Hangouts]: http://www.google.com/hangouts/
[hubot]: https://hubot.github.com/
[ChatOps]: https://speakerdeck.com/jnewland/chatops-at-github
[Lita]: https://www.lita.io/
[Webex]: http://www.webex.com/
[talky]: https://talky.io/
[Sqwiggle]: https://www.sqwiggle.com/
[Hackpad]: https://hackpad.com/
[GitHub Pull Requests]: https://help.github.com/articles/using-pull-requests/
[Gerrit]: https://code.google.com/p/gerrit/
[ReviewBoard]: https://www.reviewboard.org/
[Code Collaborator]: http://smartbear.com/product/collaborator/overview/
[Trello]: http://trello.com/
[Pivotal Tracker]: http://www.pivotaltracker.com/
[Jira's Agile Plugin]: https://www.atlassian.com/software/jira/agile#!
[Waffle]: https://waffle.io/
[GitHub Issues]: https://github.com/blog/831-issues-2-0-the-next-generation
[Etherpad]: http://etherpad.org/
[Google Docs]: https://docs.google.com/
[GitHub Wiki]: https://help.github.com/articles/about-github-wikis/
[Confluence]: https://www.atlassian.com/software/confluence/#!
[Dropbox]: http://dropbox.com/
[Box]: https://www.box.com/
[NFS]: https://en.wikipedia.org/wiki/Network_File_System_(protocol)
[WebDav]: http://webdav.org/
[Google Drive]: https://encrypted.google.com/drive/
[Exchange]: https://en.wikipedia.org/wiki/Microsoft_Exchange_Server
[Google Calendar]: https://encrypted.google.com/calendar
[Adam Savage]: https://twitter.com/donttrythis
[Carol Nichols]: https://twitter.com/carols10cents
[Skype]: http://skype.com/
[join.me]: https://join.me/

[^yagni]: This is [YAGNI] in action, in case you were wondering.
