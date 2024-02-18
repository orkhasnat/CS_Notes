#### `@lru_cache` decorator
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
The `maxsize` parameter of `lru_cache` controls the maximum number of items stored in the cache. If set to `None` (the default), the cache can grow without bounds, essentially working as `@cache` decorator. Otherwise, the cache will discard the least recently used items when it reaches the specified size.