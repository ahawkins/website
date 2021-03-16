+++
author = "Adam Hawkins"
date = 2020-08-25T02:58:56Z
draft = false
summary = "The story of Parts Unlimited as told by Bill in the Phoenix Project and Maxine in the Unicorn Project."
tags = ["podcast", "devops" ]
title = "Parts Unlimited"
toc = true
+++

_This is an episode transcript. You may also listen to the podcast
below._

{{< transistor "https://share.transistor.fm/s/a56cfe60" >}}

## Parts Unlimited

Today, I'm going to tell the story of parts unlimited parts. Parts
Unimited is a fictional company described in two different books. The
first is the Phoenix project published in 2013. And the second is the
Unicorn Project published in 2019. Both books are published by
ITRevolution press.

This is the company behind the DevOps Handbook, Accelerate, and a
bunch of other books sort of in this theme of, you know, software
delivery, business performance, operations, all this kind of stuff.

First off spoilers ahead for these two books, I'm going to just talk
about everything that happens. These are fictional books written for
software professionals and people who work in IT. They chronicle the
story of different people involved in these organizations and the
challenges and things they have to overcome and what they do and how
they react to situations, how they handle problems, this type of
stuff.

So let's begin with some context here. So parts unlimited is a auto
parts company. You can think of them like O'Reilly, Napa. They are
definitely an established business. They've been around for decades
and they are trying to come into the so-called digital world, trying
to compete with, other companies that have better online experiences,
you know, all this right? They're, kind of a representation of a old
incumbent player who needs to adopt a new ways of working and
thinking, kind of becoming what we now call a technology first company
to compete in today's market.

Both books begin at the same point, but cover different characters in
the same story. So the first book, the Phoenix project covers the
story from an ops perspective. And the second book, the unicorn
project covers the story from a development perspective.

They start in the same place. Parts Unlimited has just experienced a
huge production outage, a huge issue that has resulted in, messed up
billing, firings, really, really bad stuff. That kind of thing that
just makes you at least made me grimace and think, Oh my God, I never
want to work in a place like this. And,  luckily I haven't, but
fingers crossed that it never happens.

There's a few main characters in these books. The first character is
Bill. Bill is the reluctant a CTO who gets promoted after these
firings and ultimately is  in charge of righting the ship.

And the second book you have Maxine. Maxine is a developer who is kind
of an avatar for what we would consider a, you know, pretty good
software developer who has experienced different ways of working knows
what works knows what doesn't, you know, does things like automated
testing, continuous delivery, blah, blah.  After this shakeup, she
gets relegated to work on what is called the Phoenix project.

So the Phoenix project is a code name for then if the next generation
system of Parts Unlimited. No surprised this project is years delayed
and drastically over budget, but the company--of course--is betting
their future on this project. As the project gets delayed more and
more, it only gets delayed longer because of--well, you know, what
happens to projects that go on for a long time and never ship?

Well, the scope gets bigger. Requirements change. Things happen to
continually push back the project. As a result releases take longer.
They become more difficult. Things are more likely to break more
negative consequences, yadda yadda, yadda, this whole, negative
feedback loop of the opposite of short delivery cycles or working in
small batches.

## The Characters

That's Bill and Maxine, the two main characters from the different
books and the characters are shared across these two stories. So if
you read one or read the other, you'll see these people show up in
different ways.

One of the other main characters is Eric. He's actually my favorite
character. He's kind of this,  mysterious sensei type character. In my
mind, I kind of thought of him or at least the way he was portrayed as
some of these kind of California type hippies with long hair; driving
convertibles, living in Santa Cruz, surfing, you know, just sort of
like, ah, kind of out there, but knows what he's talking about.  They
call him a sensei and he refers, refers to other people he's learned
from as the sensei's as well.

So he guides Bill and Maxine in the two different books to different
objectives. So in the  Phoenix Project Bill guides, Eric through what
we now call the three ways of DevOps. In Unicorn Project Eric and
others guide Maxine into uncovering the five ideals which we'll  get
into later.

Brent is the engineer who is totally overloaded because he works in a
lot of different areas. He knows a lot of stuff and unfortunately many
different things have to go through Brent because he's the only one
who knows how to do it or really the only one who can get it done.
He's a bottleneck in the process for sure.

You have John who is the annoying security engineer. Who's always
trying to stop releases and inject requirements at the end of the
process that you know--in the Phoenix project they make no bones about
it. They do not like John at all.

It's really interesting to see the transformation in John, as he
realizes how much of a problem he is and that the way that he is
trying to approach his goal of improving information security is
having the exact opposite approach. And as a result, people just avoid
him and take, just, don't take him seriously.

You also have the classic executive infighting of executives and
project planners are kind of the bureaucracy of people who want this,
or don't want that. And. The people who are trying to provide cover
two different teams or empower different things in the organization.
But there is the point that these executives who represent the cross
purposes in leadership and that's a problem.

One other main character is Kurt. Kurt is a pretty smart--what was he
called, a QA engineer.  He plays a big role in both of the books as a
powerful force for getting things done.

## The Plot

The real story of these two books is the Phoenix project. So as I
mentioned earlier, the Phoenix Project is code name for the the next
generation version of the system. That they're going to release. In
order to really get out of the swamp that they're in, they need to
drastically change the ways of working.

And both these books, like I said, cover the transformation inside the
company to move away from --for want of a better term--waterfall
development and  months or years long cycles. They adopt things like,
well, the first way of DevOps, so continuous delivery, the second way
of DevOps feedback. So using information and telemetry to make
empirical decisions about what's happening. And then the third way of
DevOps experimentation and learning along with the continuous
improvement to get into this virtuous feedback loop.

That's pretty much the whole story.

So in this fictional thing, you have Parts Unlimited who is in a
horrible place in the beginning--and I've really mean horrible. If you
read this book or any of these books, you'll think, Oh my God, I don't
want to be involved in anything like this.

Then surprise, surprise. They adopt DevOps and do these things. Things
start to go well.  Everybody's happy at the end. The Phoenix project
is released. People get promotions. Everything is good. So major
success.

## The Pheonix Project

Now let's move on to the different high-level theories introduced in
both these books. So the Phoenix Project introduces the Three Ways of
DevOps. It actually came out before the DevOps Handbook. I think
DevOps Handbook was published a few years later. So in the Phoenix
project Bill uncovers the Three Ways of DevOps guided by Eric. Eric is
the experienced leader who has seen these things in practice.

Eric takes Bill through the progression of lean manufacturing into
DevOps, right? DevOps was certainly inspired by lean manufacturing. In
the book actually. This is probably one of my favorite parts about the
Phoenix Project is that Eric takes bill on gemba walks.

Gemba walk is concept from Toyota, where you go to the factory, you
see what's happening. You watch how the work happens and observe and
learn from that.

This is a real life forum to see how things work or how they don't.
Eric uses this as a training session to introduce things like the
theory of constraints to Bill to help him understand that Brent,
remember that Brent is this overloaded engineer that everything has to
go through.

So, if you imagine you're looking at a factory and you see an assembly
line, if there's a bottleneck where everything in the factory has to
go through this one choke point at that choke point is overloaded,
then. All the other things in this factory now have to wait on that.

That's an example of Eric teaching bill how Brent is a bottleneck and
that's probably one of the first things that he should work on
improving in the organization.

Eric shows Bill the Three Ways of DevOps through all these exercises
and Sort of leaving him just dead in the water sometimes when he has
questions, letting him figure out how to sink or swim for himself.

That's the Phoenix Project and the Three Ways of DevOps: flow,
feedback, and learning. We'll cover them a lot on the show. So I'm not
really gonna repeat them here. Just go to smallbatches.fm to find the
first three or four episodes of this podcast cover these things in
depth.

## The Unicorn Project

Next the unicorn project which is told from Maxine's perspective.

Maxine is the great developer. She's relegated into the Phoenix
project at the beginning of the Unicorn Project. The Unicorn Project
is effectively a code name for taking the Phoenix project And
transforming it into a better version of itself.

This is where the idea the Unicorn Project comes from because it's
almost in their mind, like impossible that this project could actually
be transformed and they could succeed. Hence the Unicorn Project.

Maxine was actually inspired by Michael Nygaard. If you don't know who
Michael Nygard is, he's a pretty awesome guy. He wrote Release it! the
first edition and now the second edition, which is a great book. Great
book. You can go to my website to Hawkins IO to find a review and
summary of Release It!

If you haven't read it, then please do. It's great. It totally changed
the way I thought about operations and releaseability. It's just
great. So do check it out if you haven't. The second edition is I
think released.one or two years ago; but it's new,  covers all the
stuff from the original book and it introduces some more stuff like
chaos engineering.

Plus, it's really fun to read. I don't know about you, but when I read
some of these tech books, they're dry, you know, they're just talking
about ideas, but the way that Michael writes, he adds just so much
life into the text. Like you can feel that this guy is with you.
You're like having a beer with him. He's telling you these stories.
It's just actually fun to read and that's rare in tech books.

Back to the Unicorn Project. Let me pull up my notes here and tell you
the progression, like sort of the outline for what happens in The
Unicorn Project.

First Maxine is exiled to the Pheonix Project as the scapegoat for the
payroll outage. Well scapegoat. Immediate red flag that they had this
whole organizational shakeup, and they had to put the blame on
somebody. Of course, Maxine didn't do anything about this, but they
needed somebody to blame. They blame Maxine. They relegate her to the
dustbin of the organization, which is the Phoenix project.

And when Maxine gets there, she can't believe the ghetto that she
finds herself in: months to get a working environment on her laptop;
there's hundreds of tickets filed and so much bureaucracy to get
anything done like getting a test environment or deploying a change to
production.

Now bear in mind that Maxine is coming from a previous working
environment where all this is at the opposite. Now she was able to
clone code, start working on her machine, start making immediate
changes. Now she's stuck on the Phoenix project, which is just months.

Actually, if I think I remember correctly in the book. Have this
internal dialogue with Maxine where she has just really frustrated,
really sad and practically, probably borderline depressed about the
whole situation. Like she wants to quit and overall just really not a
good thing.

The thing about Maxine is that she is not happy with the status quo.
That's a good thing. So she wants to do something about it. She knows
that there's  a better way to work. So she starts this, what they call
a rebellion in the company.

So what she does is she gets a bunch of people together that are
aligned to her cause and they meet at this place called the dock side
bar after work, where they go and talk about whatever happens, what to
do and all these types of things and figure out ways to bring more
people into their cause and continue to expand this rebellion in the
organization.

And their goal at the rebellion is to effectively apply DevOps to the
unicorn project. So Kurt, I mentioned earlier, he's kind of QA
manager, he's part of this rebellion and there's an internal shakeup
that allows Kurt to get his own team.

Now bear in mind that this is a hidden rebellion. People don't know
that it's happening. So. Kurt gets his team and he uses that as
organizational cover to just ignore the status quo, get things done,
and allow his team to work in whatever way is the best way possible to
deliver whatever they need to do.

One of the things I like about Kurt and this part of the Unicorn
Project is it doesn't really tell what he does, but he's a stand in
for the manager or the person kind of higher up in the organization
and knows how to play the politics effectively. Just to make sure that
his team is isolated from whatever politics and other things that are
going on that may inhibit them, such that they can just work
effectively.

So once they have this organizational cover. They start doing things
like making continuous integration, automated environment provisioning
and automated deployments.

They, being Parts Unlimited, are in a time crunch for getting the
Phoenix project out the door because you know, they're losing money
and this thing eventually has to ship at some point.

They use this to cut through a lot of the red tape required to launch
a successful black Friday promotion that demonstrates the business
value of this new way of working. And they pull this whole thing off.
It's a wild success. Everybody is happy. Maxine is promoted to a
position of distinguished engineer with a job description of
effectively what she basically did throughout the book.

Cut to black.

## The Five Ideals

Throughout this whole process she discovers what is called the five
ideals.

Let me just read off these five ideals to you.

The first one is locality and simplicity. The idea here is that you
shouldn't have to load up a huge amount of global things to make a
small pointed change.

So, again, coming back to Maxine who was previously working in a
better environment than she got into, she was able to have a code on
her machine, work with it, make a change, test it. Get it out simple,
right? Not having to provision N number of huge things and wait for
all this, but just be able to focus on local and small changes.

The next one, number two: focus, flow, and joy. This to me is the
first way of DevOps. Actually it was continuous delivery. That
developers should be able to enter the so-called flow state where
they're able to work through a problem,  focus on it, and work it in a
way that makes them happy. Key thing, being happy.

If you've worked in an organization. Where the work you do is soul
sucking or, just takes a long time, or you just think to yourself,
man, I do not want to do this. This just sucks. Well, let's avoid
that. Right? Let's create systems in a ways of working that actually
bring joy into people's work. This is what continuous delivery has
been proven to do.

They mentioned in Accelerate that continuous delivery is a direct
contributor to employee happiness and satisfaction.

Alright. Number three: improvement of the daily work. Okay. If you've
read, Mike Rother's Toyota kata. You know that what I'm getting at
with this one. The idea here is that we make the improvement of the
daily work, the daily work.

So I think this is episode. Episode four of small batches, so
smallbatches.fm/4, to learn more about the Toyota kata and improvement
of the daily work.

Ideal four: psychological safety. This is a new one for me in that the
first three, I think are,  related to DevOps and. You know, DevOps
handbook accelerate, all that.

Psychological safety is the idea that people should feel safe in their
work, like secure in the sense that they don't have to worry about
being fired for making a mistake or shipping some bug to production;
Or that the work that they do is not going to create issues.

So bringing us back to the beginning of both The Unicorn Project and
Phoenix Project: horrible, right? Somebody, some poor soul made a
mistake. We've all made mistakes.  I've shipped a plenty of bugs to
production that have had negative consequences.  I certainly wouldn't
want to be fired over that, but that's what happens at Parts
Unlimited. That's one factor of this is that you shouldn't have to
worry about huge negative ramifications from the things that are bound
to happen to every person who works in software.

And that we have to also build tools that promote a safety, like
building automated testing into the deployment pipelines. Such that we
don't ship regressions into production or we're confident that the
code or the change in question is not going to break production in any
known way.

If developers feel safe to make changes, they're more likely to make
changes. If they're more likely to make changes and more likely to
deliver on the business outcomes you're trying to achieve.

Next the fifth and final one is customer focus.  In the unicorn
project and the Phoenix project the employees have to go to one of the
physical store storefronts, right? Actual brick and mortar place where
the company. Sells parts to the customer in exchange for money. Right?
This was definitely different from working in a purely online
business.

In the Phoenix project, I think Bill goes there and gets a feel for
the current system, like the like sales system, these things that are
running in the terminals in the stores. Get a feel for the problems of
the employees and what the Phoenix project actually needs to do to
improve the workflow for these frontline employees.

And same thing in the unicorn project, Maxine goes to storefront and
sees what's happening with the software that she's  responsible for
and how that interacts or how that interplays with the frontline
employees and the end customers.

The idea behind the fifth ideal is that the developers should have
focus on the customer. So they can see that the work that they're
doing is having impact on the end users of this whole system.

## Closing Thoughts

That's the five ideals.

After I read the Unicorn Project, I started to think that, well,
there's actually a three or four, five out of a ladder here. If you
think of these things in sequence, you'll see how they all play
together.

So when I say three or four or five, I mean the three ways of DevOps:
Flow, Feedback, and Learning; the four metrics of software delivery
performance: deployment frequency, lead time, meantime to resolve, and
change failure rate; then the five ideals: locality, simplicity,
focus, flow, joy, improvement of the daily work, psychological safety,
and customer focus. So if you put these three different things
together, you have a good picture of how to think about this problem?
It's just a good framing.

I want to wrap up this episode by giving you some of my thoughts on
these two books.

First of all, I much prefer the Phoenix Project. I think that one was
much more fun to read and much more interesting. Seeing things from
Bill's perspective--this is the CTO, the manager type person--this was
far more interesting to me was this was new territory.  I also think
of the writing was better. It was just more fun.

The unicorn project. Eh;  I think you pass on it. You see some
infographic or some blog posts about the five ideals any pretty much
got the whole thing.

So take it from the other perspective. Let's say that you're a manager
and you associate yourself more with Bill and you don't really know
about how developers think. Then reading Unicorn Project would be more
interesting than reading the Pheonix Project. So now you can decide
based on what your role is which one might make more sense to you; but
I could pass on the Unicorn Project. I think that the Phoenix project
is just more fun. And. Frankly, the content of the Unicorn Project was
just more obvious to me.

## Who Should Read These Books?

So who should read these books? Since you're listening to this
podcast, you don't need to read these books anymore. Cause I think
I've given you all the information that you need to know. However, you
can recommend these books to your colleagues.

If you are interested in that from a fictional perspective Like, if
you don't want to read, say the DevOps Handbook or Accelerate, you
like reading stories, you can read both these books and get the high
level picture and then fill it in with more information by listening
to podcasts like this one or reading the books or reading blog posts,
whatever.

So recommending the Unicorn Project to managers or recommending the
Phoenix Project to more technical types, more engineers that you may
know.

## Wrap-Up

All right. I think that's enough for this episode. We've covered the
unicorn project the Phoenix project,the story of Parts Unlimited and
their transformation of adopting DevOps principles, and saving the
Phoenix project going from unprofitable, horrible place to work, to a
happy place to work that's making money; and the five ideals and the
three ways of DevOps.

If you want to learn more about these books then head to
smallbatches.fm for links. Also there's plenty of blog posts written
in depth analysis on both these books, YouTube videos and all that.

That's a wrap on this one. I'll see you again for the next episode. It
will be a special interview. So thank you for listening. See you
later.
