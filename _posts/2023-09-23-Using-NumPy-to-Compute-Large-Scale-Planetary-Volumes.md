---
layout: post
title: Using NumPy to Calculate Large-Scale Planetary Volumes
image: "/posts/planets.jpg"
tags: [Python,NumPy]
---

NumPy is a powerful linear algebra library in Python. Because it is used in a number of Python packages commonly used in data science and machine learning (such as Pandas, SciPy, Matplotlib, and Scikit-learn), NumPy is such a valuable tool to familiarize ourselves with! In this post, we will leverage NumPy's incredible efficiency performing operations on arrays to calculate the masses of *ONE MILLION* theoretical planets! 

---

First, let's use a NumPy array to store our planetary radius info. Before we jump into our million planets, let's start a little closer to home by computing the volumes for the planets in our solar system: Mercury, Venus, Earth, Mars, Jupiter, Saturn, Uranus and Neptune. (Sorry, Pluto - you will always be a planet in my heart...)

```ruby
import numpy as np

# Store solar system planet radii (in kilometers)
radii = np.array([2439.7, 6051.8, 6371, 3389.7, 69911, 58232, 25362, 24622])
```

```math
volume = 4/3 * pi * radius^3
```
One approach we might take to solve this is use a loop. It's not the most efficient way, but we'll start there and see how much we can improve upon it using NumPy's capabilities. For this approach we'll make a list that we'll call **volumes_list** and append our calculated volumes to it.

```ruby
volumes_list = []
for r in radii:
  volumes_list.append(4/3 * np.pi * r**3)
```
Let's have a look at our volumes:

```ruby
print(volumes_list)
>>> [60827208742.48264, 928415345892.8655, 1083206916845.7535, 163144485780.68842, 1431281810739357.2, 827129915150897.5, 68334355695583.96, 62525703987420.89]
```
Ok, that's a great starting point. But can we make this simpler with NumPy?

```ruby
volumes_nparray = 4/3 * np.pi * radii**3
```
We sure can! NumPy can accomplish the same result in *one fell swoop*! Let's make sure our volumes match up:

```ruby
print(volumes_list)
>>> [6.08272087e+10 9.28415346e+11 1.08320692e+12 1.63144486e+11
 1.43128181e+15 8.27129915e+14 6.83343557e+13 6.25257040e+13]
```
Same result, just with a different notation. Awesome!

Ok, time to put it to the test with our million planets. We can use NumPy's **random.randint()** to create some hypothetical planetary radii for us to use. The randint() function in NumPy takes the arguments (low, high, size), and creates *size* number of random elements ranging between *low* and *high*. Here we are creating one million random integers between 1000 and 10,000 to represent our planets' radii:

```ruby
radii = np.random.randint(1000, 10000, 1000000)
```

```ruby
np.size(radii)
>>> 1000000

print(radii)
>>> [4923 7457 7669 ... 5805 2529 5252]
```



###### Key Take-Aways: Using NumPy to perform mathematical operations on vectors is far more efficient than looping!


