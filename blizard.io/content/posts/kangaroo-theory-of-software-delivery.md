+++
title = 'Kangaroo theory of Software Delivery'
date = 2025-01-06
draft = true
+++


# The Kangaroo Theory of Software Delivery

>Imagine you're walking down a narrow alleyway. Blocking your exit is an Australian marsupial hopping the other way. Depending on the size of the animal we've got two options. If it's a wallaby we can, with some cajoling,  reorient it so it's pointing the way you want to go. If it's a kangaroo, you're stuck. It's just too big to turn around. You can try and fight it, which probably won't go well for you, or you can turn around and accept that you'll have to bend to the kangaroo's will. 

This (paraphrased) analogy was originally applied to trade negotiations between countries[^1], but it fits neatly with constraints around Software delivery too.

At every software organisation there will be seemingly iron clad rules and constraints around delivery of software.  You may have encountered some of the following; "We do not deploy on Fridays", "Every PR must be reviewed by two people", "Every change must be approved by the Change Advisory Board (CAB)", "Every change must be vetted by QA", etc. The question is: which rules are truly kangaroos – immovable obstacles that we must accept as a constraint  – and which are merely wallabies we can reorient with a bit of hard graft?

All of these rules will slow down your delivery speed.  Too many of them and you'll slow to a crawl. I have just finished at a client that had lots of these rules; I opened a PR for a one line CSS fix in my first week, and by the time I left 4 and a half months later it was still waiting to be approved by the CAB. Perhaps an extreme example, but I've worked at many clients over the course of my contracting career and you'd be surprised at how many companies do have lots of these sorts of  rules in place.

## Why Rules Exist

Of course these rules may be in place for a good reason. Operating under the principle of [Chesterton's Fence](https://en.wikipedia.org/wiki/G._K._Chesterton#Chesterton's_fence), you can't just throw away these rules for no good reason. Often a rule will be in place because of something bad that happened in the distant past, and the rule was implemented to mitigate the chances of that thing happening again. That in itself can be a sign of an org that has not sought to examine why failures happen.

In some cases, though, these ironclad rules stick around simply because _that’s how we’ve always done it_. It’s a bit like that fake “five monkeys and a ladder” experiment: a group of monkeys is put in a cage with a ladder leading up to some bananas. Whenever the monkeys go near the ladder they get blasted with water. Eventually none of the monkeys go near the ladder. One by one the monkeys get replaced, and each time the new monkey goes near the ladder the  original monkeys attack it until it stops. Eventually none of the original monkeys are left, but none of their replacements will go near the ladder. Why? Because _that’s the way it’s always been_.

The same thing happens in organisations: maybe a rule was introduced years ago to avoid a huge meltdown, but eventually nobody remembers the meltdown. They only remember “we do not deploy on Fridays—ever.”

## "We Don't Deploy on Fridays"

Let's look at an oft-used  rule. "We do not deploy on Fridays". This one is very very common, and with good reason. Shipping something on a Friday, can introduce a bug that isn't spotted until the weekend when you may be experiencing peak load, and you have fewer engineering resources to deal with it. It's easy to just say "Well, we just won't deploy on a Friday". But what if your competition does deploy on a Friday? They have 20% more time available to them to deploy something. They can release more features in a week than you can. Instead of looking at this rule as a kangaroo, maybe look at it as a wallaby and think about what work we need to do to make our Friday deployments less risky. After all, if you think Friday Deployments are risky, doesn't that say something about  the risk of *any* of your deployments? 

The problem with just accepting that a rule is a kangaroo and not a wallaby, are that we miss the opportunity to do the work in turning the wallaby around. Maybe we could deploy on a Friday if we improved our rollback process, our testing, our observability etc, but if you treat the "we don’t deploy on a Friday" rule as a kangaroo, you might never do that work, and by not doing it, all of your deployments will stay risky. For more on Friday deploys, [check out this blog post by Charity Majors](https://charity.wtf/2019/10/28/deploys-its-not-actually-about-fridays/).  

## "Every PR Must Be Manually Tested"

I encountered this rule at my last client: _no PR could be merged unless it was approved by a QA engineer._ On the face of it, that doesn’t sound too bad. After all, the client had a messy codebase resulting from years of outsourcing and inconsistent architecture—code copied and pasted everywhere. Automated testing was nearly impossible, so a thorough manual check could spot issues the original devs hadn’t anticipated.

**But not every change is functional.** Sometimes you just want to tweak the README, or add an integration test that doesn’t affect production code. Worse still, the testing team was chronically understaffed, so the developers churned out changes faster than QA could keep up. Branches became long-lived, and merging or rebasing turned into a recurring nightmare.

Making matters worse, this rule was applied to _every_ microservice—even the newer, more modern code. For instance, I created some integration tests for one of these microservices that didn’t impact application functionality at all. Yet, the QA-approval rule meant those tests sat in limbo until the testers were free to review them. Essentially, the rule became a **massive disincentive** to do the very work that would make the project more maintainable and safer to deploy.

Eventually, after much negotiation with managers and lead devs, I managed to create a set of scenarios where the lead dev could override the requirement for a QA sign-off if we agreed that the PR was non-functional. (Side note: the fact that _only_ the lead dev was allowed to review PRs is another red flag for organizational bottlenecks—but that’s a story for another day.)

## When a Kangaroo really is a Kangaroo

Sometimes a rule really is a kangaroo. Regulatory requirements in finance or healthcare, for instance, can be truly immovable. But even here, the implementation details might be wallabies. 

Next time you encounter a rule blocking your path, ask yourself – is this really a kangaroo, or just a wallaby in disguise?

[^1]: Back in 2016 the UK decided to do something dumb and [leave the EU](https://en.wikipedia.org/wiki/Brexit). Over the next few years the UK's Conservative government postured a lot about how they held all the cards in the negotiations, how many firm red lines they had, and how tough they would be in negotiating with the EU.  [Dmitry Grozoubinski](https://bsky.app/profile/explaintrade.com) came up with the Kangaroo theory of trade negotiation on his [ Explain Trade]() (https://www.explaintrade.com) blog (Original article has now sadly been removed). If i remember correctly, the theory was that when entering a negotiation each side needs to work out which items up for negotiation are kangaroos and which ones are wallabies. If you insist everything is a Kangaroo, then the negotiations will go nowhere. 
