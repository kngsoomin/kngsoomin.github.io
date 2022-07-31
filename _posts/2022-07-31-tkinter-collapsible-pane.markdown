---
layout: post
title:  "[Python][tkinter] How to create a collapsible pane?"
date:   2022-07-31 19:18:15 +0800
categories: [python, tkinter]
excerpt: "To make your frame collapsible, we need a function to change the size of the window (root) and display or hide your frame."
tags: [tkinter, python]
author: "Soomin"
---

![collapsible_page py](https://user-images.githubusercontent.com/48472921/182023765-0374d5d7-b73e-437a-9040-452a5a5cb438.gif){: width="60%" height="60%"}

To make your frame collapsible, we need a function to change the size of the window (root) and display or hide your frame.

This function will evaluate whether the frame is displayed or hidden. `Checkbutton`, a widget of tkinter.ttk, can be useful for evaluation as we can assign `tk.IntVar( )` to it. 

By default, a `Checkbutton` returns `1` when clicked, otherwise, it returns `0`. For example, if the returned value from the `Checkbutton` is `1`, you can widen the window size, display the hidden frame and change the texts in the button to ‘Collapse’. If the returned value from the button is `0`, however, you can narrow the root window and hide the frame, converting the texts in the button to ‘Expand’.


<br>
{% highlight python %}
'''Source: https://github.com/kngsoomin/tkinter-master'''

import tkinter as tk
import tkinter.ttk as ttk


def active_panel():
    if var.get():
        # Expand pane
        root.geometry('600x300') # Change the size of window
        btn_expand.configure(text=txt_collapse)
        frame_cllp.pack(side='left')
    
    elif not var.get():
        # Hide pane
        frame_cllp.pack_forget()
        root.geometry('150x300')
        btn_expand.configure(text=txt_expand)


root = tk.Tk()                 # Create new window
root.title('collapsible pane') # Set a title
root.geometry('150x300')       # A size of window when the pane is collpased
root.resizable(False, False)

s = ttk.Style()                # Create style
s.configure('pane.TButton', background='#ffffff', borderwidth=0)

# Main Frame 
frame_main = tk.Frame(root, width=300, height=300, bg='#ffffff')
frame_main.pack(side='left', fill='both', expand=True)

var = tk.IntVar()            # Initialize button for checkbutton
txt_expand = 'Expand'        # Text for button
txt_collapse = 'Collpase'    # Text for button

# Checkbutton returns default value 1 when clicked, otherwise return 0
btn_expand = ttk.Checkbutton(frame_main, style='pane.TButton',
                             text=txt_expand, 
                             command=active_panel,
                             variable=var)
btn_expand.pack(anchor='center')

# Collapsible pane
frame_cllp = tk.Frame(root, width=450, height=300)

# Image file path
path = r'C:\Users\soomi\Desktop\Soo\hiding_spongebob.png'
img = tk.PhotoImage(file=path)

# Create label for image
panel = tk.Label(frame_cllp, image=img)
panel.pack(fill = "both", expand = "yes")

root.mainloop()
{% endhighlight %}