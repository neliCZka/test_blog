---
layout: post
title:  "How to start using robot framework"
date:   2018-02-18
comments: true

---

<p class="intro"><span class="dropcap">T</span>he ultimate guide for the first steps with Robot Framework</p>


When I was a total newbie to Robot framework, I was desperately searching for "how to start with robot framework" to understand what should be the first steps and especially what should be the stucture of the test project.  
To be honest, I did not find much so I started exploring the Robot Framework on my own and started somehow.
The question is if I started right. And if I continue right... :)<br/>
I was thinking it might be just my problem and everybody else knows how to start and what to do.

But some time later a new guy was hired to another team using Robot Framework and he came to me and ask me "How to start with Robot framework?"!
Few weeks later it happened again with another new colleague.
I hope I this article might help to answer the very basic questions about RF usage. 


#### Before you start with Robot Framework
Robot Framework can run on any operating system, you just have to have Python installed and pip. 
Then you can just run this command in command line:
{% highlight bash %}
pip install robotframework
{% endhighlight %} 
(don't forget to set proxy if you do it from company network and you need it).

It is also nice to think about the **IDE** which you will use for Robot tests. I use Pycharm with Robot Framework plugin and it wokrs nicely. 
I extend Robot tests with Python, so it was the best option for me. 
Robot Framework can be extended also by Java, in that case IntelliJ Idea would be a better option for sure. :)

It is also time to think about the versiuon control, I suggest to use **GIT**. 

#### Start with the project structure

1. Create a **folder for test suites**, naming it "tests" might be a good idea :)
2. Create a **folder for lower level keywords or resources**, naming it "resources" or "keywords" could work fine
3. Create a **folder for custom libraries** which you will create in Python (or other programming language), it coud be "lib" or something like that
4. Create a **.gitignore file** in the main folder
    - add some basic file extensions of file which you don't want to track in GIT, those might be good idea:
        - &#42;.pyc
        - &#42;.png
        - &#42;.idea (if you use JetBrains IDE)
        - &#42;.html
        - &#42;.xml
        - &#42;.exe
        - &#42;.txt
        - &#42;.log
        - &#42;.iml (if you use JetBrains IDE)

This might give you a better picture of the structure of the test project. Of course, the structure does not have to be like that, but I believe it is a good practice.

#### Let's try to write first test case.

1. Create a robot file inside of "tests" folder. Name it e.g. "tests_login.robot" -> it really depends on you :)
2. Prepare the structure of the file:

{% highlight robotframework %}
*** Settings ***

Documentation     A test suite for login tests
Library    ExtendedSelenium2Library
#Resource    ../resources/resource_login.robot
#Variables  ../variables.py
#Library     ../lib/YourCustomLib.py

*** Test Cases ***

{% endhighlight %}

Now you see you have some **library** imported - in this case **ExtendedSelenium2Library** which can handle Angular frontends better than just **Selenium2Library**.
This library is an essential library for Robot Framework containing lots of useful Selenium based keywords. 

Please, be sure you have the library installed. :)
{% highlight bash %}
pip install robotframework-extendedselenium2library
{% endhighlight %} 


I added also another imports - commented now. We will get to them later.

#### Let's try to write first test case.

In the example below I use only keywords from <a href="http://robotframework.org/Selenium2Library/Selenium2Library.html">Selenium2Library</a>. 
{% highlight robotframework %}
TEST_01: Login to some page
    Open Browser    ${server}    ${browser}
    Maximize Browser Window
    Click button  ${login}
    Input Text  ${username_input}   ${username}
    Input Text  ${password_input}   ${password}
    Click button  ${submit_login}
{% endhighlight %}

#### Handle variables
You see there are lots of variables in the test case, all the structures in **${}** are variables. 
There are several ways to pass value into them:
1. Using variable file
2. Set them from the command line
3. Declare them in section: 
&#42;&#42;&#42; Variables &#42;&#42;&#42;

I believe all the ways have its own usage. So which one to choose really depends on the usage and usually more ways are combined in one project.

I can tell you how I use it:

&#49;. **Environment variables** such as ${server} and ${password} I set from **command line** so I can easily change then for each run of the tests.
The value will be passed like this:

    {% highlight bash %} 
    --variable server:https://gmail.com
    {% endhighlight %}
        

&#50;. Variables which I don't change often and which are also **related to configuration** I set in **variable file** (variables.py)
The value is passed like this:
        {% highlight python %}
        username = 'my_superuser'
        browser = 'chrome'
        {% endhighlight %}
And this case is exaclty why I have this in the test settings:

        {% highlight robotframework %}
        Variables   ../variables.py
        {% endhighlight %}

&#51;. Variables which may change often and which are **related to locators** I set in **Variables section** in each resource file
It looks like this:

{% highlight robotframework %}
*** Variables ***

${login}    //button[contains(text(),"Login")]  => this is xpath locator which might be used when no better locating is possible (e.g. some nice ID of the element)
${submit_login}   submit_login  => this means that ID or CLASS of the button element is exactly "submit_login"
{% endhighlight %}

To get the variables from another resource into the test, you have to import it as mentioned above:
{% highlight robotframework %}
Resource    ../resources/resource_login.robot
{% endhighlight %}

#### Make the tests readable

Cool, so now it is kinda clear how to work with variables I hope. Let's get back to the appearance of the test.
I believe that the best thing Robot Framework gives us is the readability of the tests. We can write supernice tests which can be used as a documentation and which can be understandable by any business stakeholder. 

The test we already wrote doesn't look very ugly, but it is not particularly nice either. 

I think business stakeholder is not very interested in reading: 
{% highlight robotframework %}
    Click button  ${login}
    Input Text  ${username_input}   ${username}
    Input Text  ${password_input}   ${password}
    Click button  ${submit_login}
{% endhighlight %}

I think this might look much better to any staeholder:
    {% highlight robotframework %}
	Log in with correct credentials
    {% endhighlight %}

So let's put all the lines under this nice keyword.<br/>
Go to the resource_login.robot file and add the steps to Keywords section:

{% highlight robotframework %}
*** Keywords ***

Log in with correct credentials
    Click button  ${login}
    Input Text  ${username_input}   ${username}
    Input Text  ${password_input}   ${password}
    Click button  ${submit_login}

{% endhighlight %}

Now change our test:

{% highlight robotframework %}
*** Settings ***

Documentation     A test suite for login tests
Library    ExtendedSelenium2Library
Resource    ../resources/resource_login.robot
Variables  ../variables.py
#Library     ../lib/YourCustomLib.py

*** Test Cases ***

TEST_01: Login to some page
    Open Browser    ${server}    ${browser}
    Maximize Browser Window
    Log in with correct credentials

{% endhighlight %}

#### Declare your test setup and test teardown
Yeeey, it is nice, right? But the stuff about opening browser is also ugly and it is kinda obvious that UI tests need to open a browser.
Do we really need to have it in every test?<br/>
I don't think so. At least in this case we want to open and maximize browser in every test, so why to repeat it all the time?<br/>
DRY (Don't Repeat Yourself) is really nice programming principle that should be followed also in test automation!

For this purpose we can setup the **test setup** which will be executed everytime. <br/>
It will change our settings section and we should also change the test itself:


{% highlight robotframework %}
*** Settings ***

Documentation     A test suite for login tests
Library    ExtendedSelenium2Library
Resource    ../resources/resource_login.robot
Variables  ../variables.py
#Library     ../lib/YourCustomLib.py

Test Setup    Run Keywords
...           Open Browser    ${server}    ${browser}   AND
...           Maximize Browser Window

*** Test Cases ***

TEST_01: Login to some page
    Log in with correct credentials

{% endhighlight %}

You see it is possible to have more keywords in test setup, it is just necessary to have 'AND' at end of each line with a keyword which is not the last one and to have '...' at the beginning of each line with keyword.

Very same can be done for **Test teardown** so you can e.g. close browser after each test run, or print console log and close the browser. 
{% highlight robotframework %}
Test Teardown    Close Browser
{% endhighlight %}

Now you might think that the test looks way too short, but this is just very basic test, so why not to have it short? Anyway, we still miss some other step to verify, that we were logged to really correct page etc., so the real test would be bigger for sure. 


#### Run the test
All right, now we have everything prepared, so how to run the test and see it works?

Easy, just go to your terminal and get to the root of the project. 
Type:
{% highlight bash %}
robot --variable server:https://gmail.com --variable password:some_super_pass tests/tests_login.robot
{% endhighlight %}
And you should see new browser window opened and it should start clicking instead of you! Yipeee! 

How do you use Robot Framework? What were your first steps and what is your test project structure? <br/>
Share the knowledge in the comments! :)




