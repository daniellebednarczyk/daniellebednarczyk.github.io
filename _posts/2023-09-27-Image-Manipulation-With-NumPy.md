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
![Book logo](/least-github-pages/assets/logo.png)

```

```ruby

>>> 
```

---

Sure, it's easy for me to get excited by this. After all, I am a data nerd that optimizes processes for fun. But, I hear you hypothetically asking, what actual benefit does this optimization bring to the table? And you are right to ask! 

<span style="color:#f58506;font-weight:bold;">Efficiency</span>: Speed matters in the business world. Faster computing procedures allow a business to process data and perform tasks much more quickly. This means faster decision-making, quicker response times to customer inquiries, and a more efficient workflow.

<span style="color:#f58506;font-weight:bold;">Competitive Advantage</span>: In today's competitive landscape, being faster can be a significant competitive advantage. If our business can deliver products or services more quickly or analyze data faster than competitors, it can attract more customers and gain market share.

<span style="color:#f58506;font-weight:bold;">Cost Savings</span>: Faster procedures often require fewer computing resources and less energy. This can translate into cost savings for the business. Reduced computing time means lower cloud computing or server/resource costs, which can be especially important for businesses with large-scale data processing needs.

<span style="color:#f58506;font-weight:bold;">Real-time Insights</span>: Speedy computations enable real-time data analysis. This is crucial for industries like finance, e-commerce, and logistics, where timely insights can lead to better investment decisions, personalized customer experiences, and optimized supply chain operations.

<span style="color:#f58506;font-weight:bold;">Scaling Possibilities</span>: Fast procedures are more scalable. As our business grows, we can handle larger volumes of data or transactions without a proportional increase in computing resources or time. This scalability is crucial for handling growth without a proportional increase in costs.

<span style="color:#f58506;font-weight:bold;">Innovation and Productivity</span>: Faster computations free up time and resources for innovation. Our data scientists and analysts can spend less time waiting for results and more time exploring data, developing new algorithms, and finding creative solutions to business challenges.

---


