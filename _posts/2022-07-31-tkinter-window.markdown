---
layout: post
title:  "[Python][tkinter] How to create a window"
date:   2022-07-31 16:55:15 +0800
categories:
    - python
excerpt: "How to create a window and kickstart tkinter"
tags:
    - python
    - tkinter
author: "Soomin"
---

`root.mainloop( )` loops forever waiting for the event from the users until the program is terminated by either keyboard interruption or closing the window.

<br>
{% highlight python %}
import tkinter as tk

root = tk.Tk()                # Create new window
root.title('Hello, Tkinter!') # Set program title
root.geometry('600x300')      # width=600, height=300
root.resizable(False, False)  # Prevent users to resize the window
root.mainloop()               # Loops forever`
{% endhighlight %}