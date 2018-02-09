---
layout: post
title:  "Beauty of API tests"
date:   2017-12-25
---

<p class="intro"><span class="dropcap">I</span>f you are a developer, you will probably not understand why I write this article, because beauty of API tests is just obvious.</p>


But try to imagine you are a manual tester. All you do is just manual cliking in the application and preparing test cases in some bad tool like HPQC or even excel back in some ancient ages. The heaven is not the limit, but the physical and psychical state of the tester is. The run time of the test depends just on the tester and it usually takes some time to do even a smoke test. So usually you have the test results in hours. 

#### Wow effect of automated test

Then imagine you write your first automated UI tests. "It" clicks instead of you! It generates the results instead of you! It genereates the report! It can be ran so many times! WOW, that's just amazing! And yes, it is pretty amazing, but to be honest, speed of automated UI test is never really good. It takes almost the same ages as manual execution of the test. It still needs to wait for javascript to load, it must click here and there etc. So you still have the results in long minutes or even hours in case of bigger sets.

#### Even bigger wow effect of API test

And finally now, imagine you write your first API test. Oh my god, that's not just amazing, it is incredible! You just run the test now and you have the result in few seconds! All the "order creation" or whatever is done in supersonic speed it seems. You don't have to wait for hours or long minutes, you have the results in seconds! And what's even better, you know exactly what is the expected behavior and what should be returned in the response for any request, so it is much easier to debug API tests and also the tests are much more stable than UI  tests. I won't lie, it is a wet dream of every tester, so the wow effect is really huge. 

#### Who should do it?

But who is the one to define the API tests? Is it a developer or a tester in the team?
I believe it depends. If you join a team as a tester and there are no API tests, I strongly encourage you to start the automation with them. It helps you to understand the application way better and it will give you instant results after each deploy and you might have more time to prepare UI tests. And also, you can enjoy this wonderful joy of writing API tests, because it is usually much easier and straight forward than UI tests which are always failing in some weird way (at least from the beginning).
If you join a team where API tests are done and developers prepare them during development of new feature, you can still check whether they cover only happy path and if so, you can help them to extended the tests by negative ones.
I believe API tests stand between pure development part and pure business part of the project, so I would not say they must be defined only by developers or only by testers. I guess the team should choose what works the best for them. I just think it is necessary to have them, because API tests cover the business functionality much better than unit tests and they are much faster and much easier to implement than UI tests, so why not to take this advantages?


