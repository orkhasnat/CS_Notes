# Built-In Functions
-  **[[Zip Function in Python|zip function]]**

# Built-In Modules
- **[[Itertools Module in Python|Itertools]]**
- **[[Functools Module in Python|Functools]]**
- **[[Collection Module in Python|Collection]]**

# Misc. Concepts
- **[[Nested Functions in Python#Closures|Closure]]**
- **[[Nested Functions in Python#Decorators|Decorators]]**
	- **[[Nested Functions in Python#Decorators|Built-In Decorators]]**
# Syntactical Sugar
### Walrus `:=` Operator
The walrus operator allows you to ==assign a value== to a variable as ==part of an expression==. It is particularly useful in situations where you need to both compute a value and use it in a condition or expression.
Without the walrus operator:
```python
number = 0
while number < 5:
    print(number)
    number += 1
```
With walrus operator,
```python
number = 0
while (number := number + 1) < 5:
    print(number)
```


