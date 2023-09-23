---
layout: post
title: Using NumPy to Calculate Large-Scale Planetary Mass
image: "/posts/planets.jpg"
tags: [Python,NumPy]
---

NumPy is a powerful linear algebra library in Python. Because it is used in a number of Python packages commonly used in data science and machine learning (such as Pandas, SciPy, Matplotlib, and Scikit-learn), NumPy is such a valuable tool to familiarize ourselves with! In this post, we will leverage NumPy's incredible efficiency performing operations on arrays to calculate the masses of *ONE MILLION* theoretical planets! That's a **MASS**ive amount! (I'll show myself out...)

---

First, let's use a NumPy array to store our planetary radius info. Before we jump into our million planets, let's start a little closer to home by computing the masses (in km) for the planets in our solar system: Mercury, Venus, Earth, Mars, Jupiter, Saturn, Uranus and Neptune. (Sorry, Pluto - you will always be a planet in my heart).

```python
import numpy as np

radii = np.array([2439.7, 6051.8, 6371, 3389.7, 69911, 58232, 25362, 24622])
```

```math
volume = 4/3 * pi * radius^2
```

```ruby
number_range = set(range(2, n+1))
```

Let's also create a place to store any primes we discover.  A list is perfect for this.

```ruby
primes_list = []
```

We're going to end up using a while loop to iterate through our list and check for primes, but before we construct that I find it valuable to code up the logic and iterate manually first. This gives us the opportunity to check that it is working correctly before it runs through everything on its own.

So, we have our set of numbers (called number_range) to check all integers between 2 and 20. Let's extract the first number from that set so we can start checking if it is a prime. If it is, we're going to add it to our list called primes_list. If it is not a prime, we don't want to keep it.

There is a method which will remove an element from a list or set and provide that value to us, and that method is called *pop()*

```ruby
print(number_range)
>>> {2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20}
```
If we use *pop()* and assign this to an object we'll call **prime**, it will *pop* the first element from the set out of **number_range**, and into **prime**

```ruby
prime = number_range.pop()
print(prime)
>>> 2
print(number_range)
>>> {3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20}
```

We know that the very first value in our range is 2, and that it is going to be a prime. So, let's add it to our list of primes.

```ruby
primes_list.append(prime)
print(primes_list)
>>> [2]
```

Now we're going to do a neat trick that will check our remaining number_range for non-primes, and allow us to eliminate them. For the prime number we just checked (in this first case it was the number 2), we want to generate all the multiples of that number up to our upper range (in our case, 20). These multiples by definition cannot be prime numbers, because they are wholly divisible by more combinations than themselves and 1.

We're going to again use a set rather than a list. A set allows us some special functionality that we'll use soon, which is the neat part of this approach.

```ruby
multiples = set(range(prime*2, n+1, prime))
```

Remember when we create a range the syntax is range(start, stop, step). For the starting point, we don't need our number as that has already been added as a prime, so let's *start* our range of multiples at 2 * our number. In our case here our number is 2, so the first multiple will be 4. If the number we were checking was 3 then the first multiple would be 6 - and so on.

For the *stop* point of our range - we specify that we want our range to go up to 20, so we use n+1 to specify that we want 20 to be included.

Now, the **step** is key here. We want multiples of our number, which means we want to increment in steps *of our* number, so we use **prime** here

Lets have a look at our list of multiples...

```ruby
print(multiples)
>>> {4, 6, 8, 10, 12, 14, 16, 18, 20}
```

The next part is the coolest bit - we're using the special set functionality **difference_update**, which removes any values from our number range that are multiples of the number we just checked. The reason we're doing this is because if a number is a multiple of anything other than 1 or itself then it is **not a prime number**, and we can remove it from the list to be checked.

Before we apply the **difference_update**, let's look at our two sets.

```ruby
print(number_range)
>>> {3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20}

print(multiples)
>>> {4, 6, 8, 10, 12, 14, 16, 18, 20}
```

**difference_update** works in a way that will update one set to only include the values that are *different* from those in a second set.

To use this, we call **difference_update** on our **number_range**, and pass it our set of **multiples**. This will keep everything in **number_range** that is not in **multiples**, essentially eliminating our known non-primes from our **number_range**.

```ruby
number_range.difference_update(multiples)
print(number_range)
>>> {3, 5, 7, 9, 11, 13, 15, 17, 19}
```

When we look at our number range now, all values that were also present in the multiples set have been removed as we *know* they were not primes.

This is amazing! We've made a massive reduction to the pool of numbers that need to be tested, so this is really efficient. It also means the smallest number in our range *is a prime number*, as we know nothing smaller than it divides into it...and this means we can run all that logic again from the top!

A while loop is a great way to run this process through our **number_range**. We can have it do the heavy lifting of updating the number list and extracting primes until the list is empty.

Let's run it for any primes below 1000...

```ruby
n = 1000

# number range to be checked
number_range = set(range(2, n+1))

# empty list to append discovered primes to
primes_list = []

# iterate until list is empty
while number_range:
    prime = number_range.pop()
    primes_list.append(prime)
    multiples = set(range(prime*2, n+1, prime))
    number_range.difference_update(multiples)
```

Let's print the primes_list to have a look at what we found!

```ruby
print(primes_list)
>>> [2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97, 101, 103, 107, 109, 113, 127, 131, 137, 139, 149, 151, 157, 163, 167, 173, 179, 181, 191, 193, 197, 199, 211, 223, 227, 229, 233, 239, 241, 251, 257, 263, 269, 271, 277, 281, 283, 293, 307, 311, 313, 317, 331, 337, 347, 349, 353, 359, 367, 373, 379, 383, 389, 397, 401, 409, 419, 421, 431, 433, 439, 443, 449, 457, 461, 463, 467, 479, 487, 491, 499, 503, 509, 521, 523, 541, 547, 557, 563, 569, 571, 577, 587, 593, 599, 601, 607, 613, 617, 619, 631, 641, 643, 647, 653, 659, 661, 673, 677, 683, 691, 701, 709, 719, 727, 733, 739, 743, 751, 757, 761, 769, 773, 787, 797, 809, 811, 821, 823, 827, 829, 839, 853, 857, 859, 863, 877, 881, 883, 887, 907, 911, 919, 929, 937, 941, 947, 953, 967, 971, 977, 983, 991, 997]
```

Let's now get some interesting stats from our list which we can use to summarize our findings, the number of primes that were found, and the largest prime in the list:

```ruby
prime_count = len(primes_list)
largest_prime = max(primes_list)
print(f"There are {prime_count} prime numbers between 1 and {n}, the largest of which is {largest_prime}")
>>> There are 168 prime numbers between 1 and 1000, the largest of which is 997
```

Awesome!

The next thing to do would be to put it into a tidy function, which you can see below:

```ruby
def primes_finder(n):
    
    # number range to be checked
    number_range = set(range(2, n+1))

    # empty list to append discovered primes to
    primes_list = []

    # iterate until list is empty
    while number_range:
        prime = number_range.pop()
        primes_list.append(prime)
        multiples = set(range(prime*2, n+1, prime))
        number_range.difference_update(multiples)
        
    prime_count = len(primes_list)
    largest_prime = max(primes_list)
    print(f"There are {prime_count} prime numbers between 1 and {n}, the largest of which is {largest_prime}")
```

Now we can jut pass the function the upper bound of our search and it will do the rest!

Let's go for something large, say a million...

```ruby
primes_finder(1000000)
>>> There are 78498 prime numbers between 1 and 1000000, the largest of which is 999983
```

That is pretty cool!

I hoped you enjoyed learning about primes, and one way to search for them using Python.

---

###### Important Note: Using pop() on a Set in Python

In the real world we would need to make a consideration around the pop() method when used on a Set as in some cases it can be a bit inconsistent.

The pop() method will usually extract the lowest element of a Set. Sets however are, by definition, unordered. The items are stored internally with some order, but this internal order is determined by the hash code of the key (which is what allows retrieval to be so fast). 

This hashing method means that we can't 100% rely on it successfully getting the lowest value. In very rare cases, the hash provides a value that is not the lowest.

Here we're just coding up something fun, but it is certainly a useful thing to note when using Sets and pop() in Python in the future!

The simplest solution to force the minimum value to be used is to replace the line...

```ruby
prime = number_range.pop()
```

...with the lines...

```ruby
prime = min(sorted(number_range))
number_range.remove(prime)
```

...where we firstly force the identification of the lowest number in the number_range into our prime variable, and following that we remove it.

However, because we have to sort the list for each iteration of the loop in order to get the minimum value, it's slightly slower than what we saw with pop().


