# Built-In Functions
-  **[[Zip Function in Python|zip function]]**

# Built-In Modules
- **[[Itertools Module in Python|Itertools]]**
- **[[Functools Module in Python|Functools]]**
- **[[Collection Module in Python|Collection]]**

# Misc. Concepts
- **[[Nested Functions in Python#Closures|Closure]]**
- **[[Nested Functions in Python#Decorators|Decorators]]**
	- **[[Nested Functions in Python#Built-In Decorators|Built-In Decorators]]**
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

### `*args` & `**kwargs`
`*args` and `**kwargs` are special syntax in Python used in function definitions to allow a variable number of arguments. 
###### \*args:
- The `*args` syntax in a function definition allows you to pass a variable number of non-keyword arguments to the function.
- The `args` name is a convention, and you can use any name preceded by an asterisk (`*`).
- It collects extra positional arguments as a tuple.
###### \*\*kwargs:
- The `**kwargs` syntax allows you to pass a variable number of keyword arguments to the function.
- The `kwargs` name is a convention, and you can use any name preceded by double asterisks (`**`).
- It collects extra keyword arguments as a dictionary.
- The special syntax `**kwargs` in function definitions in Python is used to pass a key worded, variable-length argument list.
> [!info] Keyword Argument 
> - A keyword argument is where you provide a name to the variable as you pass it into the function.
> - One can think of the *kwargs* as being a dictionary that maps each keyword to the value that we pass alongside it. That is why when we iterate over the *kwargs* there doesn’t seem to be any order in which they were printed out.
```python
# Example 1: function argument passing
def myFun(*args, **kwargs):
	print("args: ", args)
	print("kwargs: ", kwargs)

myFun('geeks', 'for', 'geeks', first="Geeks", mid="for", last="Geeks")
```
```python
# Example 2: set values of object
class Person:
    def __init__(self, *args, **kwargs):
        self.name = args[0] if args else kwargs.get('name', 'Unknown')
        self.age = args[1] if len(args) > 1 else kwargs.get('age')
        self.city = kwargs.get('city', 'Unknown')
        
person1 = Person('Alice', 25, city='New York')
person2 = Person(name='Bob', age=30, city='San Francisco')
```

### Unpacking using `*` and `**`
1. `*` unpacks iterables.
```python
tuple1 = (1, 2, 6)
tuple2 = (4, 5, 3)

combined_tuple = (*tuple1, *tuple2)
# Output: (1, 2, 6, 4, 5, 3)
```
2. `**` unpacks dictionaries.
```python
dict1 = {'name': 'John', 'age': 25}
dict2 = {'city': 'New York'}

combined_dict = {**dict1, **dict2}
#Output: {'name': 'John', 'age': 25, 'city': 'New York'} 
```