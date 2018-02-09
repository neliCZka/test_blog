---
layout: post
title:  "Test 3rd party component in automated tests?"
date:   2017-12-24
---

<p class="intro"><span class="dropcap">S</span>ome time ago I was in a discussion with developers about what to test by my automation tests and what not to test.</p>

I had some issues automating 3rd party component reused in the application which I tested. I needed some explanations and changes from our developers to make the automation easier. Well, in fact not easier, but doable at all. 
Instead of some working solution I got answer like this: 

"You should not test 3rd party component. It is not our code and it does not make sense to test someone else's code. It should not be your goal. You should believe that the component is widely used and almost bug free. We could provide you with the data you need to test in some hidden structure so you can avoid testing the 3rd party component."

Hmm. I was thinking. It was a lot of suggestions and I was thinking about it from many angles and I was not sure how to react immediately. So I just said something like "OK, I will think about it, it might make sense, but my tests should test exactly the same what the end user can see, but yes, it might be correct and much easier approach."

#### Should we give up on E2E tests?

Of course it would be much easier approach. But it is not what E2E tests should do. Go the easy way, use hidden structures and then just hope that it is also correctly displayed to end user. 
So I should have said strict NO. No, we cannot use this approach, because user does not use any hidden structure. User will see the data applied in the component we use. We can definitely do API tests which could cover the data layer test, but only as an extension (and very powerful one) to our E2E UI tests.
Everytime you hear suggestions like that, you should see the big STOP sign in your head and try to explain what is the real goal of the tests. Even if it is not said by anyone, but you think about an easy solution for E2E UI tests. Because unfortunately there is not any easy solution to test an application in the same way as would user do. 

Another reason why we should test even 3rd party component is that we can never be sure that the component is used in correct way in our application. Or if the data are loaded correctly. So it is not about testing the 3rd party component, but about testing our whole application, no matter if some part is written by internal developers or reused from outside. 