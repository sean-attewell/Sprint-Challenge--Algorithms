Add your answers to the Algorithms exercises here.

## Exercise I

Give an analysis of the running time of each snippet of
pseudocode with respect to the input size n of each of the following:

```
a)  a = 0
    while (a < n * n * n):
      a = a + n * n
```

This while loop **looks** like it would increase by O(n^3), but because a is increasing at a rate of O(n^2), it actually only runs n times. If n is 1 it will run once, if n is 2 it will run twice, if n is 3 it will run 3 times.  
Therefore the time complexity is linear: O(n).

```
b)  sum = 0    # O(1)
    for i in range(n):    # O(n)
      i += 1    # O(1)
      for j in range(i + 1, n):    # O(n)
        j += 1    # O(1)
        for k in range(j + 1, n):    # O(n)
          k += 1    # O(1)
          for l in range(k + 1, 10 + k):    # O(1)
            l += 1    # O(1)
            sum += 1    # O(1)
```

The statements are performed n^3 times due to the nested iteration. Constants get cancelled out.  
1 + n _ n _ n _ 2 _ 1 => 1 + O(2n^3) => O(n^3)  
Time complexity = O(n^3)

```
c)  def bunnyEars(bunnies):
      if bunnies == 0:    # O(1)
        return 0

      return 2 + bunnyEars(bunnies-1)    # O(n)
```

If bunnies is 1, it will call itself recursively once. If bunnies is 2, it will call itself recursively twice. If bunnies is 3 it will call itself recursively 3 times. Therefore the runtime scales linearly with n.  
Time complexity = O(n)

## Exercise II

Suppose that you have an _n_-story building and plenty of eggs. Suppose also that an egg gets broken if it is thrown off floor _f_ or higher, and doesn't get broken if dropped off a floor less than floor _f_. Devise a strategy to determine the value of _f_ such that the number of dropped eggs is minimized.

Write out your proposed algorithm in plain English or pseudocode and give the runtime complexity of your solution.

We could use binary search here - because the floors are already in order from lowest to highest, we don’t need to search them all. Instead we can start with the middle index and see if the egg breaks. If it does not break then we can eliminate that floor and all floors below it, and try the middle of the new set of higher floors. If it does break, then we can eliminate the floors above it because it will break on those too (but keep the floor we are on this time in case it happened to be the lowest breaking floor by chance), and try the middle of the floors below it. Each time we repeat this process we have half the number of things to check this way.
Runtime complexity = O(log(n))
