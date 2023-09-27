---
layout: post
title: Image Manipulation With NumPy
image: "/posts/Bomber_Dog.jpg"
tags: [Python, NumPy, Image Manipulation]
---

Let's have a little fun in this post and explore working with images in NumPy! There are libraries in Python that can do this for us, but I always find it helpful to explore what's going on under the hood to understand it better.

---

We're going to need to import some libraries and modules to load and display our images. The **io** package from the **skimage** library allows us to import an image. From the **Matplotlib** library we are going to import **pyplot** as plt, which is a fairly standard naming convention for that package.
// TODO: make sure I used package/library/module properly there



```python
import numpy as np
from skimage import io
import matplotlib.pyplot as plt
```

A note about imports:
Notice how we imported things a few different ways?
// TODO: Describe why using this as a reference: https://www.codingem.com/python-difference-between-import-and-from-import/

            
I'm saving the image I want to work with to my working directory in Python, so we do not have to reference its full address when uploading.

```ruby
bdog = io.imread("Bomber_Dog.jpg")
```

Our image is imported as a NymPy array. Images are just a series of numbers representing the intensity of each colour channel (R, G, B) for each pixel.

Let's take a look at the shape of our array:


```ruby
bdog.shape
>>> (995, 1500, 3)
```
We have a 3-dimensional array, representing our rows, columns, and RGB values (which are between 0 and 255 for each of the three colour channels). This image has 995 rows of pixels and 1500 colums of pixels, so it's wider than it is tall.

Now let's take a look at our image:

```ruby
plt.imshow(bdog)
plt.show()
```
![alt text](/img/posts/image_manipulation_with_numpy/bdog_plot.png "Coffee & Python - I love them!")

Since we're going to be viewing our image a lot as we go, I'm going to toss those two lines of code into a function so we only need to call one line of code each time. We'll pass the image we want shown as an argument, that way we can send any image we want to it.
```python
def show_image(image):
    plt.imshow(image)
    plt.show()
```
Let's see what we can do with this image using NumPy!

First, let's crop it a little, so BomberDog and "his" Jeep are a little more prominant. We can slice our array to crop the image. Let's start by cropping just one axis, and see what we get:

```ruby
cropped = bdog[0:500,:,:]
show_image(cropped) 
```

---


---


