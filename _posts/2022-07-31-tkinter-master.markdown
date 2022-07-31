---
layout: post
title:  "[tkinter] How to create a window"
date:   2022-07-31 16:55:15 +0800
categories: python-tkinter
---
# [tkinter] How to create a window
`root.mainloop( )` loops forever waiting for the event from the users until the program is terminated by either keyboard interruption or closing the window.

`import tkinter as tk

root = tk.Tk()                # Create new window
root.title('Hello, Tkinter!') # Set program title
root.geometry('600x300')      # width=600, height=300
root.resizable(False, False)  # Prevent users to resize the window
root.mainloop()               # Loops forever`