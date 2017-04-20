---
layout: post
title:  "Noooo! Stop CMD-Q Quitting the App"
date:   2017-04-11 17:20:00
categories: mac
excerpt: "How to prevent CMD-Q quitting your app on a Mac."
---

I do my development on a Mac and usually have multiple things going on at one time, so there are often 3 or 5 Atom editor windows open on various desktops, and often even more Terminal windows scattered across the different desktops too. Not to mention at least one Chrome window on each desktop. I very often switch back and forth between windows using `CMD-tab`. However, with the `tab` key being so close to `Q`, I sometimes hit the `Q` instead of the `tab`.

### 😱 😱 😱 Nooooooooooo! 😱 😱 😱 ###

Whichever app was on top is now GONE! All of the windows, too! Yikes! Of course we can get them back, but it is extremely annoying to be interrupted so rudely in the middle of working on something.

### 🤔 There must be a better way! 🤔 ###

After doing some investigating, I decided to map the special key combination for inverting colors to be `CMD-Q`.

**Here's how:** Go to `Apple->System Preferences...` then select `Keyboard`, then `Shortcuts` and finally, click on `Accessibility` in the left column. Once there, click the box next to `Invert Colors` as shown here.

![Keyboard Shortcuts]({{ site.baseurl }}/assets/images/keyboardShortcuts1.png)

Now, click on the characters to the right of `Invert Colors` and enter `CMD-Q`. Now when you accidentally do `CMD-Q`, the screen will harmlessly invert its colors, which might be a little surprising, but no harm done! Just do `CMD-Q` again to return the colors back to normal.

![Changed Keyboard Shortcuts]({{ site.baseurl }}/assets/images/keyboardShortcuts2.png)

I know there are other ways to change key mappings, but this seemed like the easiest to do overall. I'm using  OSX El Capitan, so if you are on a different version, your windows might look a bit different.
