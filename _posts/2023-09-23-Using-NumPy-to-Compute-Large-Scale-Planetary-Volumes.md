---
layout: post
title: Using NumPy to Calculate Large-Scale Planetary Volumes
image: "/posts/planets.jpg"
tags: [Python,NumPy]
---

NumPy is a powerful linear algebra library in Python. Because it is used in a number of Python packages commonly used in data science and machine learning (such as Pandas, SciPy, Matplotlib, and Scikit-learn), NumPy is such a valuable tool to familiarize ourselves with! In this post, we will leverage NumPy's incredible efficiency performing operations on arrays to calculate the masses of *ONE MILLION* theoretical planets! 

---

First, let's use a NumPy array to store our planetary radius info. Before we jump into our million planets, let's start a little closer to home by computing the masses (in km) for the planets in our solar system: Mercury, Venus, Earth, Mars, Jupiter, Saturn, Uranus and Neptune. (Sorry, Pluto - you will always be a planet in my heart).

```python
import numpy as np

radii = np.array([2439.7, 6051.8, 6371, 3389.7, 69911, 58232, 25362, 24622])
```

```math
volume = 4/3 * pi * radius^2
```

---

###### Key Take-Aways: Using NumPy to perform mathematical operations on vectors is far more efficient than looping!


