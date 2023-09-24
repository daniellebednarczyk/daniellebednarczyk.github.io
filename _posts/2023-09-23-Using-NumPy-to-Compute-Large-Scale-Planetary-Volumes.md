---
layout: post
title: Using NumPy to Calculate Large-Scale Planetary Volumes
image: "/posts/planets.jpg"
tags: [Python,NumPy]
---

NumPy is a powerful linear algebra library in Python. Because it is used in a number of Python packages commonly used in data science and machine learning (such as Pandas, SciPy, Matplotlib, and Scikit-learn), NumPy is such a valuable tool to familiarize ourselves with! In this post, we will leverage NumPy's incredible efficiency performing operations on arrays to calculate the masses of *ONE MILLION* theoretical planets! 

---

First, let's use a NumPy array to store our planetary radius info. Before we jump into our million planets, let's start a little closer to home by computing the volumes for the planets in our solar system: Mercury, Venus, Earth, Mars, Jupiter, Saturn, Uranus and Neptune. (Sorry, Pluto - you will always be a planet in my heart...)

```python
import numpy as np

# Store solar system planet radii (in kilometers)
radii = np.array([2439.7, 6051.8, 6371, 3389.7, 69911, 58232, 25362, 24622])
```

```math
volume = 4/3 * pi * radius^3
```
One approach we might take to solve this is use a loop. It's not the most efficient way, but we'll start there and see how much we can improve upon it using NumPy's capabilities. For this approach we'll make a list that we'll call **volumes_list** and append our calculated volumes to it.

```python
volumes_list = []
for r in radii:
  volumes_list.append(4/3 * np.pi * r**3)
```
We can see that our volumes

```
print(volumes_list)
>>> [60827208742.48264, 928415345892.8655, 1083206916845.7535, 163144485780.68842, 1431281810739357.2, 827129915150897.5, 68334355695583.96, 62525703987420.89]
```

---

###### Key Take-Aways: Using NumPy to perform mathematical operations on vectors is far more efficient than looping!


