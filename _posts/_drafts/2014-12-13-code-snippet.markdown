---
layout: post
title:  "Manual test cases in Robot Framework"
date:   2017-12-28
comments: true

---

<p class="intro"><span class="dropcap">M</span>anula test cases don't have to be a pain when you don't keep them separated from automatino framework.</p>



Just recently I was exploring options how to manage manual tests on a project I've been participating. There were some suggestions to use HPQC ALM - well, I would rather write the tests into stones than using ALM these days and in agile environment. I wanted to use JIRA and some extension, but it was not possible from "security" reasons. And then I heared about possibility to use Robot Framework. Wait, what? Robot Framework? That automation framework? 
Oh yes, exactly that automation framework. Some of my colleagues were just exploring "Dialogs" library which allows manual step run and user inputs to the test execution. Wow. I was so excited I had to try it immediately. 
And it is really quite nice if you already use Robot Framework for test automation as we do.

I see mainly these benfits in using Robot Framework also for manual test cases:

1. There can be only one repository for all the tests - automated and manual. So we can actually store all the tests in one GIT repo! Whole structure is then more clear and you can use all the advantages of GIT.

2. You have unified test reports from both automated and manual tests. And I have to say that Robot's reports are very good and informative so it would be great to have the same report also for manual tests.

3. You will have the high level tests cases prepared for automation. Yes. That's maybe the best benefit, because by manual test you already define the test case steps which need to be done so it motivates you to make it automated as soon as possible. Let's be honest, it is sometimes way too painful to automate some old regression tests from the beginning, but if it is already in Robot and you are looking at them all the time. And it is also perfect way how to start Acceptance Test Driven Development in your team!

4. You can define setup and teardown as for automated tests which can make the manual tests much faster. You can also automate more steps. Or you can have just one step manual - the one which is difficult to automate perhaps. But of course, you cannot include such test into Continuous Integration pipeline. :) You can also use all the cool features of Robot like tags, logging and much more. 

5. When manual step fails, you may input text description of the failure. You can input also link to defect or anything you want to include into the report. 


But I am just at the very beginning of using this approach and I can already see some things which may be improved. For example passing more steps at once and I will probably find some more needs. But it can be still extended by own library etc. So we may have so many new options! :)
So let's try this if you don't have any other smooth setup for manual tests...