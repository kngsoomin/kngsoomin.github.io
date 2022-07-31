---
layout: post
title:  "[Python][tkinter] How to create a splash screen (loading page) with GIF?"
date:   2022-07-31 19:04:15 +0800
categories:
    - python
excerpt: "A splash screen is a particular screen that pops up when you first run the program."
tags:
    - python
    - tkinter
author: "Soomin"
---

![splash screen](https://user-images.githubusercontent.com/48472921/182023413-76ecf19e-07b5-430f-a337-cc2e848d3a10.gif){: width="50%" height="50%"}

A splash screen is a particular screen that pops up when you first run the program.

To add a splash screen in tkinter, you may create a new window, put it on a timer, and then destroy it after the timer runs out. 

To make your splash screen more attractive with animation, you can insert the GIF into it. Given that the GIF file will be read as a set of multiple frames, you can utilize the recursive function to loop through the frames in GIF.

You can read GIFs from the URL or your local directory to insert in the splash screen. 

1. [Guide to create a splash screen](https://youtu.be/LTVvHObxc4E)
1. [Guide to display GIFs in tkinter](https://youtu.be/ZX-5XQ1Q8Zg)


<br>
{% highlight python %}
'''Source: https://github.com/kngsoomin/tkinter-master'''

import tkinter as tk
import tkinter.ttk as ttk


class App(tk.Tk):
    
    def __init__(self):
        tk.Tk.__init__(self)             # Create the main window
        self.resizable(False, False)     # Set the window unresizable
        
        container = tk.Frame(self)       # Create the main frame to store frames
        container.pack(fill='both', expand=True)
        
        self.frames = {}                 # Initialize dict to store frames
        self.framesize = {}              # Initialize dict to store frame sizes
        
        # Loop to initialize all frames 
        for F in (PageA, PageB, PageC):
            page_name = F.__name__
						# New frames will be created in container frame in controller window
            frame = F(parent=container, controller=self) 
            self.frames[page_name] = frame
            self.framesize[page_name] = frame.size
            frame.grid(row=0, column=0, sticky='nsew')
            frame.grid_propagate(0)
            
        self.show_frame('PageA')          # Show PageA as the first page
 
    def show_frame(self, page_name):
        # Get the size of frame to display
        frame_size = self.framesize[page_name]
        
        # Change the window size to the frame size
        self.geometry(frame_size)
       
        # Show the frame
        frame = self.frames[page_name]      
        frame.tkraise()
                


class PageA(tk.Frame):
    
    def __init__(self, parent, controller):
        tk.Frame.__init__(self, parent, bg='grey', width=200, height=200)
        self.size = '200x200'
        lbl = tk.Label(self, text='PageA', bg='grey')
        lbl.grid(row=0, column=0)
        btn = tk.Button(self, 
                        text='>> PageB', 
                        command=lambda: controller.show_frame('PageB'))
        btn.grid(row=1, column=0)
        
        
        
class PageB(tk.Frame):
    
    def __init__(self, parent, controller):
        tk.Frame.__init__(self, parent, bg='#ccccff', width=150, height=150)
        self.size = '150x150'
        lbl = tk.Label(self, text='PageB', bg='#ccccff')
        lbl.grid(row=0, column=0)
        btn = tk.Button(self, 
                        text='>> PageC', 
                        command=lambda: controller.show_frame('PageC'))
        btn.grid(row=1, column=0)
        
        
        
class PageC(tk.Frame):
    
    def __init__(self, parent, controller):
        tk.Frame.__init__(self, parent, bg='#ffcc99', width=300, height=150)
        self.size = '300x150'
        lbl = tk.Label(self, text='PageC', bg='#ffcc99')
        lbl.grid(row=0, column=0)
        btn = tk.Button(self, 
                        text='>> PageA', 
                        command=lambda: controller.show_frame('PageA'))
        btn.grid(row=1, column=0)


root = App()
root.mainloop()
{% endhighlight %}