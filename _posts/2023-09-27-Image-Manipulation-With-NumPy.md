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
![Plot of Dog on Jeep](/img/posts/image_manipulation_with_numpy/bdog_plot.png "Plot output of our image")

Since we're going to be viewing our image a lot as we go, I'm going to toss those two lines of code into a function so we only need to call one line of code each time. We'll pass the image we want shown as an argument, that way we can send any image we want to it.
```python
def show_image(image):
    plt.imshow(image)
    plt.show()
```
So now we can just call *show_image()* and pass it the NumPy array of our image: 
```ruby
show_image(bdog)
```
![Plot of Dog on Jeep](/img/posts/image_manipulation_with_numpy/bdog_plot.png "Plot output of our image")

Let's see what we can do with this image using NumPy!

---
In this first section let's get our feet wet doing some simple slicing on our image array. I'd like to crop it a little, so BomberDog and "his" Jeep are a little more prominant. We can slice our array to crop the image. Let's start by cropping just one axis, and see what we get. **Note**: when we are slicing our array, using a colon **:** signifies to keep all values.

```ruby
cropped = bdog[0:500,:,:]
show_image(cropped) 
```
![Partially cropped plot of Dog on Jeep](/img/posts/image_manipulation_with_numpy/bdog_first_crop.png "Plot output of our partially cropped image")
    
Ok, we've confirmed that the first axis that we refer to in our slicing is the Y-axis. In other words, we've cropped vertically. Let's try cropping along the horizontal axis:

```ruby
cropped = bdog[:,450:1350,:]
show_image(cropped)
```
![Partially cropped plot of Dog on Jeep](/img/posts/image_manipulation_with_numpy/bdog_second_crop.png "Plot output of our partially cropped image")

And we've confirmed that the second axis is cropping along the X-axis of our image. Now that we know what we have to do to crop along the X and Y axes of our image, let's try and crop out some of the background and finish getting our subjects framed. Remember that our third dimension is for our RGB values, and we don't want to mess around with those...for now...

```ruby
cropped = bdog[235:950,450:1350,:]
plt.imshow(cropped)
plt.show()
```
![Fully cropped plot of Dog on Jeep](/img/posts/image_manipulation_with_numpy/bdog_full_crop.png "Plot output of our fully cropped image")

We'll come back to this image a little later and do some other fun stuff with it! For now, let's save it:

```ruby
io.imsave("bdog_cropped.jpg", cropped)
```

---

In this next section let's explore flipping or "mirroring" our image.

We can use the *start, stop, step* notation when retrieving a dimension of our array. Using a *step* of -1 will reverse the order in which the elements are retrieved. Doing this to our first dimension will reverse the rows, but we will leave our columns and colour channels untouched.

```ruby
vertical_flip = bdog[::-1,:,:]
show_image(vertical_flip)
```
![Vertically flipped plot of Dog on Jeep](/img/posts/image_manipulation_with_numpy/bdog_vertical_flip.png "Plot output of our vertically flipped image")

Of course we can flip it horizontally as well:

```ruby
horizontal_flip = bdog[:,::-1,:]
show_image(horizontal_flip)
```
![Horizontally flipped plot of Dog on Jeep](/img/posts/image_manipulation_with_numpy/bdog_horizontal_flip.png "Plot output of our horizontally flipped image")

At first glance it might not look like it has been flipped, but notice that the LMTV (large military truck) is now on the right side of the image instead of the left.

---


