---
layout: post
title: Tkinter를 이용해서 Image Loader 구현해보기
category: Python
tag: [Python, tkinter]
---
# Tinker를 이용해서 Image Loader 구현해보기

<pre class="prettyprint">
import tkinter as tk

images = ["01.png", "02.png"]


class ImageViewer():

    def __init__(self, window):
        self.canvas = tk.Canvas(window, width=1280, height=800)
        self.canvas.grid(row=0, column=0)

        self.button = tk.Button(window, text="Load Image", command=self.on_button_clicked)
        self.button.grid(row=1, column=0)

        self.img = None
        self.image_on_canvas = self.canvas.create_image(0, 0, anchor=tk.NW)
        self.image_idx = 1

    def on_button_clicked(self):
        self.img = tk.PhotoImage(file=images[self.image_idx])
        self.canvas.itemconfig(self.image_on_canvas, image=self.img)
        self.image_idx = 1 - self.image_idx
        pass


window = tk.Tk()
window.title("Image Viewer Sample")
ImageViewer(window)
window.mainloop()
</pre>