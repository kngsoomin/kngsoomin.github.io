---
layout: post
title:  "[Python][tkinter] Difference between the widgets of tkinter and tkinter.ttk"
date:   2022-07-31 18:33:15 +0800
categories: 
    - python
excerpt: "While tkinter widgets are configurable and well documented, the widgets of tkinter.ttk are nicer and smoother looking as they are customizable."
tags:
    - python
    - tkinter
author: "Soomin"
---

Basically, `tkinter.ttk` supports a variety of widgets as compared to `Tkinter` widgets. While `tkinter` widgets are configurable and well documented, the widgets of `tkinter.ttk` are nicer and smoother looking as they are customizable. 

When exploring `tkinter`, you will notice some widgets are provided by `tkinter` while others are from `tkinter.ttk`. There are even widget types provided by both `tkinter` and `tkinter.ttk`.

For instance, the code below causes several `tkinter.ttk` widgets (Button, Label, Frame, Entry, Checkbutton, Radiobutton, etc.) to automatically replace the Tk widgets.


<br>
{% highlight python %}
from tkinter import *
from tkinter.ttk import *
{% endhighlight %}

Replaced widgets look nicer with a broader range of configurations, however, the replacement widgets are not completely compatible. One noticeable difference is that styling options for widgets like `fg` and `bg` are no longer available for `tkinter.ttk` ([Source](https://docs.python.org/3/library/tkinter.ttk.html#using-ttk)). Instead, we may define `ttk.Style` to customize styling effects. 

You can utilize widgets of `tkinter` and `tkinter.ttk` together in one program!