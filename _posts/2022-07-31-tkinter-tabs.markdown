---
layout: post
title:  "[Python][tkinter] How to create multiple tabs and bind action to tab change?"
date:   2022-07-31 19:33:15 +0800
categories:
    - python
excerpt: "Tabbed widgets can be created using Notebook. To define action on tab change, you can bind a function to Notebook as shown in the example codes below."
tags:
    - python
    - tkinter
author: "Soomin"
---

![multi-tabs](https://user-images.githubusercontent.com/48472921/182024314-aad489d5-8635-4164-90f4-12617b703039.gif){: width="50%" height="50%"}

Tabbed widgets can be created using Notebook. 

To define action on tab change, you can bind a function to Notebook as shown in the example codes below. 

In this example, as the tab changes, the number of tab changes is counted and packed as a label with a randomly selected background color.

<br>
{% highlight python %}
'''Source: https://github.com/kngsoomin/tkinter-master'''

import tkinter as tk
import tkinter.ttk as ttk
import random


def update_label_and_change_bg(event):
    '''Define action for tab change'''
    
    global idx_tab1, idx_tab2
    tabname = event.widget.tab('current')['text']  # Get current tab name
    
    if tabname == 'tab1':
        idx_tab1 += 1
        label = tk.Label(tab1, text=f'You selected tab1 for \'{idx_tab1}\' times')
        label.pack()
                
    if tabname == 'tab2':
        idx_tab2 += 1
        label = tk.Label(tab2, text=f'You selected tab2 for \'{idx_tab2}\' times')
        label.pack()

    # Get random color hex 
    color = '#%06x' % random.randint(0, 0xFFFFFF)
    # Change label background
    label.config(bg=color)
       
       
# Create root window
root = tk.Tk()
root.geometry('300x300')
root.title('tkinter - Tabs')

# Create tab controller
tabControl = ttk.Notebook(root)

# Create tabs and add to controller
tab1 = ttk.Frame(tabControl)
tab2 = ttk.Frame(tabControl)
tabControl.add(tab1, text='tab1')
tabControl.add(tab2, text='tab2')

# Initalize index
idx_tab1 = 0
idx_tab2 = 0

# Pack tabs
tabControl.pack(expand=1, fill='both')

# Bind function to tab change
tabControl.bind('<<NotebookTabChanged>>', update_label_and_change_bg)

root.mainloop()
{% endhighlight %}