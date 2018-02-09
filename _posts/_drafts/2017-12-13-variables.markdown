---
layout: post
title:  "Don't mess up with variables in Robot Framework"
date:   2017-12-09
comments: true
---

<p class="intro"><span class="dropcap">V</span>ariables will be your best friend in Robot tests, so don't treat them with no respect.</p>

When I started with Robot Framework, I was looking for some examples how to write the tests. And as I was getting quite quickly into use of Robot Framework, it happened that I started declaring the variables in multiple ways.
It was working, of course, but your test project does not look good if it does not have a unified structure of variable declaration.
I don't even remember why I dared to use spaces in the variable names, maybe I thought it looks more user friendly?  It loooks more like a human senctence then? Maybe, but now I don't think so at all. 

Soon I ended up with some variables written in upper case, some in lower case, some as snake case, some just with spaces:

{% highlight robotframework %}
***  Variables ***

${SAVE BUTTON}	save
${EDIT_BUTTON}	edit
${delete button}	//button[@name='delete']  
${cancel_buttton}	cancel
{% endhighlight %}

#### The power is in the unity

If I may suggest, use just lower snake case, because it seems to be natural, understandable and most widely used as it is pythonic (so of course, if you don't like python, you can use camelCase instead :):
{% highlight robotframework %}
***  Variables ***

${delete_button}	//button[@name='delete']  
${cancel_buttton}	cancel
{% endhighlight %}

In this case you can also easily switch from robot variables to python variables or command line variables if you decide to. If you declare the variables with spaces instead of underscore and then use it like that, it won't be clear what variable you are declaring in python file because the actual use of the variable will be with spaces, but declaraion will be with underscore and that's confusing.

Also beware that you should not declare one variable multiple times - e.g. if you declare variable in Robot file,
{% highlight robotframework %}
***  Variables ***

${username}    some_username 
{% endhighlight %} 
then also declare the variable in Python file: 
{% highlight python %}
username = 'some_username' 
{% endhighlight %} 
and then you declare it even from command line like 
{% highlight bash %}
--variable username:some_username
{% endhighlight %} 

It is probably gonna work, it will apply the variable declared in command line, but hey, it means you don't have the tests in control. You say the variable may have 3 different values, what's the truth then?
How can you trust such tests?

