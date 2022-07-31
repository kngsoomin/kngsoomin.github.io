---
layout: post
title:  "[Python][tkinter] How to create multiple pages - (1) create multiple windows"
date:   2022-07-31 18:39:15 +0800
categories:
    - python
excerpt: "If you want to create a program consisting of multiple windows, you can generate the instance of TopLevel class."
tags:
    - python
    - tkinter
author: "Soomin"
---

![top-level](https://user-images.githubusercontent.com/48472921/182022597-8be66a29-6564-44e8-9cf6-b9e31beb2e77.png){: width="60%" height="60%"}

You can build a GUI program with multiple pages by creating multiple windows.

In tkinter, the main window is the instance of `Tk class`, which can be created with `tk.Tk( )`. When you destroy the main widow, the main loop ends, and it terminates the program.  

Then, what if you want to have multiple windows and want to keep the loop even if you destroy them?

If you want to create a program consisting of multiple windows, you can generate the instance of TopLevel class. Unlike the main window, you can create as many top-level windows as you want. On top of that, the main loop will remain running even if you close the top-level windows.

I refer to this [link](https://www.pythontutorial.net/tkinter/tkinter-toplevel/#:~:text=How%20it%20works.,the%20Close%20button%20is%20clicked.&text=Third%2C%20in%20the%20open_window(),that%20it%20can%20receive%20events.) for the post.


<br>
{% highlight python %}
'''
Source: https://www.pythontutorial.net/tkinter/tkinter-toplevel/#:~:text=How%20it%20works.,the%20Close%20button%20is%20clicked.&text=Third%2C%20in%20the%20open_window(),that%20it%20can%20receive%20events.
'''
import tkinter as tk
from tkinter import ttk


class Window(tk.Toplevel):
    def __init__(self, parent):
        super().__init__(parent)

        self.geometry('300x100')
        self.title('Toplevel Window')

        ttk.Button(self,
                text='Close',
                command=self.destroy).pack(expand=True)


class App(tk.Tk):
    def __init__(self):
        super().__init__()

        self.geometry('300x200')
        self.title('Main Window')

        # place a button on the root window
        ttk.Button(self,
                text='Open a window',
                command=self.open_window).pack(expand=True)

    def open_window(self):
        window = Window(self)
        # window.grab_set()    
        # If you uncomment above line, you can prevent
	# users from interacting with the Main Window

if __name__ == '__main__':
    app = App()
    app.mainloop()
{% endhighlight %}