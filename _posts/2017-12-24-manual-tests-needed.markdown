---
layout: post
title:  "Is manual testing still needed these days?"
date:   2017-12-24
---

<p class="intro"><span class="dropcap">A</span>s the time to market has been getting shorter and shorter recently, the need for fast automated testing is rising.</p>


One could say that manual testing is the bottleneck which slows whole development cycle down. One may think manual testing has no place in agile teams, the less in continuous delivery. 
And it is true in some point, there is really need to speed the proccess up, to cover as much as possible with automated tests. And that's good because automated tests can be ran anytime, as many times as needed and they are independent on one's mood, physical or psychical state.
But can we really automate everything? And do we really want to do that?

I don't think so. 

#### Scope of automated tests

Automated test can cover only what we define to cover. And it will repeat the same test all around. But as we know, tests must be changed from time to time to find new bugs, to check the app from a diffent angle. And can we really do that? Do we have time to change already existing and so nicely passing tests? Maybe we have time, but do we have a courage to do it? 

Not always.

At some point we might think we have even achieved 100% test coverage. Wow, that's great, that's the main goal right? 
Well, I would't say.
What defines 100% test coverage? We can measure this for unit tests, but never for E2E tests or for usability tests. Because there are always scenarios behind the obvious ones which we might discover just accidentally. And that's it. That's the human element which is so great and important. In your automated test you will not introduce any human error probably. But when you use the app as an user, you can do some wrong steps leading you to very unexpected behavior of the app. And that's exactly what might happen to end user even if your app has 100% test coverage with all tests passing...

#### God bless human's imperfections

And it is not just about exploring human error based bugs, but also usability. Usability cannot be tested by any tool even if it uses some smart algorithm taking all the UX rules in count. Why? Because we don't. We as users don't care about the UX rules which were written in some books etc. Of course, we follow most of them without even knowing, but everyone has different habits, different preferences and this is the key for usability testing. More people, different people, they try, they argue and they can eventually find out the best solution.

There might be also some diffcult cases for which automation would take ages. Honestly, is it really better to spend a week automating something user can test in a minute just to get closer to 100% test coverage? And what about maintanance of such difficult test cases? And as I said, high test coverage does not have to mean anything in fact...

Because lots of tests can be coverd by automation, manual testers should focus on exploratory testing and usability testing. It is wonderful how human can go through the app and explore all the corners. But manual testers should also feel strong responsibility otherwise exploratory testing may end up exploring nothing.


To sum this up, I think manual testing has still its place in development cycle and it's going to last, perhaps, forever. 
Of course, what can be effectively automated, should be automated. But we should involve the human element into testing as well. And those manual testers should be proud of themselves, because they've beaten "the machines" at certain point. 
