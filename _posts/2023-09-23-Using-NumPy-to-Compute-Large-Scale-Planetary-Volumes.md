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
We sure can! NumPy can accomplish the same result in *one fell swoop*! We simply plug in our NumPy array for our value of radius in our equation. NumPy will apply the calculation to EACH value in our array. Let's make sure our volumes match up:

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

Let's confirm we do in fact have one million entries, and take a peek at some of the values to see what they look like:

```ruby
np.size(radii)
>>> 1000000

print(radii)
>>> [4923 7457 7669 ... 5805 2529 5252]
```

Looking good! Ok, the moment of truth. Let's plug our NumPy array of one million radii into our equation for **r** (radius) again:

```ruby
volumes = 4/3 * np.pi * radii**3
```
The calculation completes so quickly, I want to double-check the size and values of our **volumes** array to make sure it everything was actually computed!

```ruby
np.size(volumes)
>>> 1000000
print(volumes)
>>> [-3.96094440e+09 -8.17465329e+09  2.91678988e+08 ... -8.17425859e+09
 -4.20884318e+09 -4.86035823e+09]
```
And there they are! 

NumPy is so much faster, I think it would be really interesting to time each method. That way we can also have a measurable metric with which to compare them, so you don't have to just take my word for it!

I'm going to use the *timeit* library in Python. It enables us to time the execution of a snippet of code, and gives us the ability to run each process a designated number of times so we can get a more accurate idea of how long the process might typically take. For the sake of this experiment, I'm going to loop each process 1000 times. We'll make a variable for our number of iterations called **i** and set it to 1000. We can use this variable when we call our **timeit()** function on each code snippet.

```python
import timeit
i = 1000
```

First, our loop. By putting our multiple lines of code that loop through our array and compute volume into a single function called **vol_calc()**, we can call it as a single argument in the **timeit** method. Let's call our loop time **t_loop** so we can compare it later on.

```ruby
volumes_list = []
def vol_calc():
    for r in radii:
        volumes[r] = 4/3 * np.pi * r**3
t_loop = timeit.timeit('vol_calc()', globals=globals(), number=i)
```

Our **t_loop** time value is for the total amount of time it took to run the 1000 iterations of our code snippet. In order to get the time it takes for a single execution of computing our one million entries using a loop, we need to divid our total time by the number of times we executed the code (our **i** iterations variable, which in this case is 1000).

```ruby
print(t_loop / i)
>>> 1.2878372399951332
```
So it takes  roughly 1.27 seconds to compute our million theoretical planetary volumes by iterating through our **radii** array and adding each volume to our **volumes** list.

We already know our NumPy vector operation is much faster. But **HOW** much faster? Let's let **t_np** be the total time it takes to compute our one million volumes using a NumPy array operation in **i** iterations (which is still 1000).  

```ruby
t_np = timeit.timeit('volumes = 4/3 * np.pi * radii**3', globals=globals(), number=loop)
print(t_np / i)
>>> 0.002873580000596121

print(print(t_loop / t_np)
>>> 448.1647421432404
```
**WOW**! That is ***ALMOST 450 TIMES FASTER!!!***

---

Sure, it's easy for me to get excited by this. After all, I am a data nerd that optimizes processes for fun. But, I hear you hypothetically asking, what actual benefit does this optimization bring to the table? And you are right to ask! 

**Efficiency**: Speed matters in the business world. Faster computing procedures allow a business to process data and perform tasks much more quickly. This means faster decision-making, quicker response times to customer inquiries, and a more efficient workflow.

**Competitive Advantage**: In today's competitive landscape, being faster can be a significant competitive advantage. If our business can deliver products or services more quickly or analyze data faster than competitors, it can attract more customers and gain market share.

**Cost Savings**: Faster procedures often require fewer computing resources and less energy. This can translate into cost savings for the business. Reduced computing time means lower cloud computing or server/resource costs, which can be especially important for businesses with large-scale data processing needs.

**Real-time Insights**: Speedy computations enable real-time data analysis. This is crucial for industries like finance, e-commerce, and logistics, where timely insights can lead to better investment decisions, personalized customer experiences, and optimized supply chain operations.

**Scaling Possibilities**: Fast procedures are more scalable. As our business grows, we can handle larger volumes of data or transactions without a proportional increase in computing resources or time. This scalability is crucial for handling growth without a proportional increase in costs.

**Innovation and Productivity**: Faster computations free up time and resources for innovation. Our data scientists and analysts can spend less time waiting for results and more time exploring data, developing new algorithms, and finding creative solutions to business challenges.

---

<span style="color:#f58506;font-weight:bold;"> Key Take-Aways</span>: Using NumPy to perform mathematical operations on vectors is hundreds of times more efficient than looping. These sorts of optimizations can have tangible and profound advantages for businesses.


