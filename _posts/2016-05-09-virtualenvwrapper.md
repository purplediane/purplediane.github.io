---
layout: post
title:  "Python Virtualenvwrapper Tool 👍"
date:   2016-05-09 16:17:39
category: lightningtalk
excerpt: "A very simple introduction to the virtualenvwrapper tool."
---
I'd like to introduce you to a cool tool that you can use to manage Python projects, called **[`virtualenvwrapper`][venvwrapper]**.

These are the slides from a Lightning talk I gave at the San Diego Python Meetup in March 2016.

![Title slide]({{ site.baseurl }}/assets/images/Virtualenvwrapper.001.jpeg)

You are probably already aware of virtual environments, or "virtualenvs" that allow you to use different versions of Python and Python packages. Last fall, when I was working with [Trey Hunner][th] with materials for the Python class he was teaching, I discovered the existence of `virtualenvwrapper` and was excited to find out how useful it can be.

I try to be organized, and keep my projects and virtualenvs where I can find them. But I was finding it difficult to remember what I named projects and venvs.
Especially when following various tutorials that do things a little differently.

![Haz Projects]({{ site.baseurl }}/assets/images/Virtualenvwrapper.002.jpeg)

Now with `virtualenvwrapper`, I can always find my projects and virtualenvs.

### Step 1. Install It

![Step 1]({{ site.baseurl }}/assets/images/Virtualenvwrapper.003.jpeg)

### Step 2. Simple Set-up

![Step 2]({{ site.baseurl }}/assets/images/Virtualenvwrapper.004.jpeg)

### Step 3. Create a Project

![Step 3]({{ site.baseurl }}/assets/images/Virtualenvwrapper.005.jpeg)

### Later on...

![Later On]({{ site.baseurl }}/assets/images/Virtualenvwrapper.006.jpeg)

The best part comes later, when you've been away from the project, the terminal window's been closed, and you've forgotten the details of the project. Say you called the project `newapp` when you created it with the `virtualenvwrapper` tool. All you have to do to get back to it is type `workon newapp`. Voilá! Your virtual environment is activated and you are dropped into the newapp project directory, ready to get to work!

### Find Your Projects

![Find Projects]({{ site.baseurl }}/assets/images/Virtualenvwrapper.007.jpeg)

This is one of the best parts! I don't always remember what I called a project - I try to make the names mean something but I also like them to be short & sweet. So sometimes it's a mystery to me what I might have called a project. With `virtualenvwrapper`, mystery solved!

### Create Just a virtualenv

![Create virtualenv]({{ site.baseurl }}/assets/images/Virtualenvwrapper.008.jpeg)

### Other Commands

![Other Commands]({{ site.baseurl }}/assets/images/Virtualenvwrapper.009.jpeg)

If you have several projects that are related (so you want to use a different project file structure from virtualenvwrapper's default), and they have different virtualenvs, you can create the virtualenvs with `mkvirtualenv`. Then, when you have the project file structure the way you like it, you can use `setvirtualenvproject` from each of the project folders to associate them to the virtualenv. Then when you use `workon` to activate a virtualenv, it will put you into the correct project folder.

### Further Readings

![Further Readings]({{ site.baseurl }}/assets/images/Virtualenvwrapper.010.jpeg)

Here is a clickable link: [`virtualenvwrapper`][venvwrapper]

### Caveats

![Caveats]({{ site.baseurl }}/assets/images/Virtualenvwrapper.011.jpeg)

### Thanks for reading!

I hope this has helped you with `virtualenvwrapper`! I have found it a very useful tool and for me it has been great. I like to go through lots of tutorials and this is a good way to keep them separated and keep track of them.

[venvwrapper]: http://virtualenvwrapper.readthedocs.org/en/latest/
[th]: http://treyhunner.com/
