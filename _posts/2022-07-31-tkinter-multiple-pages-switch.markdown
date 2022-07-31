---
layout: post
title:  "[Python][tkinter] How to create multiple pages - (2) create multiple frames and switch"
date:   2022-07-31 18:53:15 +0800
categories: [python, tkinter]
excerpt: "The first thing to do is to create the main window (controller) and the main frame (container). Next, initialize all frames (instances of tk.Frame) and place them within the main frame (container)."
tags: [tkinter, python]
author: "Soomin"
---

![ezgif com-gif-maker](https://user-images.githubusercontent.com/48472921/182022794-def5c9ec-1c32-462b-ac37-b2dd2c956eb9.gif){: width="40%" height="40%"}

Creating multiple frames and switching between them within a single main window is another way to achieve the goal.  

The first thing to do is to create the main window (`controller`) and the main frame (`container`).
Next, initialize all frames (instances of `tk.Frame`) and place them within the main frame (`container`).
The last thing to do is to define a method for switching the frame and changing the size (geometry) of the root window (`controller`) based on the target frame. 

By using this method of `controller`, you can switch between multiple frames.  

I refer to this [link](https://stackoverflow.com/questions/7546050/switch-between-two-frames-in-tkinter) for the post.


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