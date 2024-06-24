# `@lru_cache` Decorator
The `functools` module provides the `lru_cache` decorator, which stands for "Least Recently Used Cache." This decorator is used to cache the results of a function, saving time by avoiding redundant computations for previously seen arguments. Additionally, it helps manage the cache size, discarding the least recently used entries when the cache reaches a specified limit.
```python
from functools import lru_cache

@lru_cache(maxsize=6)
def fib(n):
    if n <= 1:
        return n
    return fib(n-1) + fib(n-2)

print(fib(10))
```
# `@cache` Decorator
The `maxsize` parameter of `lru_cache` controls the maximum number of items stored in the cache. If set to `None` (the default), the cache can grow without bounds, essentially working as `@cache` decorator. Otherwise, the cache will discard the least recently used items when it reaches the specified size.

# `reduce()` Function
The `reduce()` function in Python applies a rolling computation to sequential pairs of values from an iterable, reducing it to a single value.
### Function Signature
```python
from functools import reduce

reduce(function, iterable[, initializer])
```
- `function`: The function that defines the computation to be performed. It should take two arguments.
- `iterable`: The iterable (e.g., list, tuple, etc.) to be reduced.
- `initializer`: Optional initial value for the computation. If provided, `reduce()` will use this as the first argument to the function when reducing.
### How `reduce()` Works
1. **Initialization**: If an `initializer` is provided, it serves as the initial value for the computation. Otherwise, the first two elements of the `iterable` are used as the initial arguments to `function`.
2. **Iterative Computation**: The `function` is applied to the current cumulative result and the next element of the `iterable`. This process repeats sequentially until all elements of the `iterable` have been processed.
3. **Final Result**: `reduce()` returns the final accumulated value after applying the `function` to all elements of the `iterable`.

### Examples
##### 1. Calculating the Sum of Numbers
```python
from functools import reduce

numbers = [1, 2, 3, 4, 5]
sum_all = reduce(lambda x, y: x + y, numbers)
print(sum_all)
```
**Output:** `15`
> Alternately, we could have used the `sum` builtin function.
##### 2. Finding the Maximum Number
```python
from functools import reduce

numbers = [3, 8, 1, 6, 5, 7, 2]
max_num = reduce(lambda x, y: x if x > y else y, numbers)
print(max_num)
```
**Output:** `8`
> Alternately, we could have used the `max` builtin function.
### Handling Edge Cases
- **Empty Iterables**: If `reduce()` is called with an empty iterable and no `initializer`, it raises a `TypeError`. If an `initializer` is provided, it returns the `initializer` as the result.
- **Single Element Iterables**: If the iterable has only one element and no `initializer` is provided, `reduce()` returns that single element without calling the function.
### Why Use `reduce()`?
- **Rolling Computation**: Useful for operations that require cumulative results over a sequence, such as computing sums, products, maximum or minimum values, etc.
- **Compact and Readable**: Provides a concise way to express iterative computations compared to traditional loops.

For generating lists based on iterative operations, list comprehensions are often more intuitive and ***Pythonic***. Thus they might be preferred over the `reduce` function.