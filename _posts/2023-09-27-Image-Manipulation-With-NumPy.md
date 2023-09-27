---
layout: post
title: Image Manipulation With NumPy
image: "/posts/Bomber_Dog.jpg"
tags: [Python, NumPy, Image Manipulation]
---



---

```ruby

```



```ruby

```


```ruby

>>> 
```

```

```ruby
prime_count = len(primes_list)
largest_prime = max(primes_list)
print(f"There are {prime_count} prime numbers between 1 and {n}, the largest of which is {largest_prime}")
>>> There are 168 prime numbers between 1 and 1000, the largest of which is 997
```


---

###### Important Note: 



...with the lines...

```ruby
prime = min(sorted(number_range))
number_range.remove(prime)
```

...where we firstly force the identification of the lowest number in the number_range into our prime variable, and following that we remove it.

However, because we have to sort the list for each iteration of the loop in order to get the minimum value, it's slightly slower than what we saw with pop().

