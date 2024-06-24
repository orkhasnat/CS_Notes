Nested Functions, also called as **Inner Functions** are functions that you define inside other functions. In Python, this kind of function has direct access to variables and names defined in the enclosing function. Inner functions have many uses, most notably as closure factories and decorator functions.
The basic features of inner functions are,
- Provide **encapsulation** and hide your functions from external access
- Write **helper functions** to facilitate code reuse
- Create **closure factory functions** that retain state between calls
- Code **decorator functions** to add behavior to existing functions

These are all ***higher order functions***.
## Closures
```python
def outer(x):
    def inner(y):
        return x + y
    return inner

add_five = outer(5) # x=5
result = add_five(6) # y=6
print(result)  # prints 11
```
The `add_five` is an object with `outer` function and the value for `x=5` together. At that point `outer` has only the definition of `inner` in it, but nothing has been called. Think `add_five` as an alias for `outer` with argument `x` equals to `5`. Here `add_five` is a ***closure***.
> [!tip]- Closure
> Closures are dynamically created functions that are returned by other functions. Their main feature is that they have full access to the variables and names defined in the local namespace where the closure was created, even though the enclosing function has returned and finished executing.
> ==I.e. Closures retain states.==

Now when result is calculated, then `outer` returns its returning object which coincidentally is a function that takes the value `y=6`. Think of it as the following, 
- `outer(5): outer(5)->{inner,x=5}` Imagine `outer` as a black box that takes `5` as  input and returns `{inner}` object as an output.
- `add_five(6): 6->{inner,x=5}->{inner(6),x=5}` Then this `{inner}` object takes `6` as an input all the while having other values inside it.
- `result: {inner(6),x=5} => {return x+y,y=6,x=5} => {return 5+6} =>  11` In the end, all the wrappings are unwrapped and we get a solid integer value `11`.
##### Closure, How?
In the above example, the `inner` function is defined inside the `outer` function. The `inner` function *"closes over"* the variable `x` from the outer scope, meaning it retains access to the value of `x` even after the `outer` function has finished executing. When `add_five` function is created by calling `outer(5)`, essentially a closure is created where `x` is set to 5. Later, when `add_five(6)` is called, the `y` parameter takes the value 6, and the closure allows access to the `x` value from the outer scope, resulting in the sum of 5 and 6, which is 11.

## Decorators
Decorators are the most common use of higher-order functions in Python. It allows programmers to modify the behavior of function or class. Decorators allow us to wrap another function in order to extend the behavior of wrapped function, without permanently modifying it. In Decorators, functions are taken as the argument into another function and then called inside the wrapper function.
In the above example if `outer` took a *function as a parameter then it would be a decorator*.
```python
def outer(func):
    def inner():
        print("I got decorated")
        func()
    return inner
    
def ordinary():
    print("I am ordinary")
    
# decorate the ordinary function // closure
decorated_func = outer(ordinary)
# call the decorated function
decorated_func()
```
```
Output:
I got decorated
I am ordinary
```
#### @ Symbol With Decorator
Instead of assigning the function call to a variable, Python provides a much more elegant way to achieve this functionality using the `@` symbol. For example,
```python
def outer(func):
    def inner():
        print("I got decorated")
        func()
    return inner
    
@outer
def ordinary():
    print("I am ordinary")

ordinary()  # outer(ordinary)()
```
#### Decorators with Parameters
```python
def smart_divide(func): # this line changed
    def inner(a, b):
        print("I am going to divide", a, "and", b)
        if b == 0:
            print("Whoops! cannot divide")
            return
        return func(a, b) # this line changed
    return inner

@smart_divide
def divide(a, b):
    print(a/b)

divide(2,5)
divide(2,0)
```
```
Output:
I am going to divide 2 and 5
0.4
I am going to divide 2 and 0
Whoops! cannot divide
```
Another way we can create decorators is as follows, 
```python
def my_decorator_with_args(arg):
    def decorator(func):
        def wrapper():
            print(f"Decorator argument: {arg}")
            func()
        return wrapper
    return decorator

@my_decorator_with_args("example")
def say_hello():
    print("Hello!")

say_hello()
```
#### Chaining Decorators
Multiple decorators can be chained in Python. To chain decorators in Python, we can apply multiple decorators to a single function by placing them one after the other, with the **most inner decorator being applied first**.
```python
@star
@percent
def printer(msg):
    print(msg)
```
The above is equivalent to below,
```python
def printer(msg):
    print(msg)
printer = star(percent(printer))
```

### Built-In Decorators 
###### `@classmethod` decorator
- Is used to define class methods in a class.
- Class methods take a reference to the class itself as their first parameter, conventionally named `cls`.
- **Similar to the `static` keyword in C++.**
```python
class MyClass:
    x = 10
    
    @classmethod
    def print_private_var(cls):
        print(cls.x)
        
MyClass.print_private_var()
```
###### `@property` decorator
- The `@property` decorator is used to define **getter methods** in a class.
- It allows us to access a method like an attribute without calling it explicitly.
- In addition to `@property`, we can use the `@property_name.setter` decorator to define a **setter method**.
```python
class Geek: 
	def __init__(self): 
		self._name = 0

	@property
	def name(self): 
	print("Getter Called") 
	return self._name 

	@name.setter 
	def name(self, name): 
	print("Setter called") 
	self._name = name 

p = Geek() 
p.name = 10
print(p.name)
```
```
Output:
Setter called 
Getter Called
10
```
###### `@cache` decorator from `functools`
Basically `@lru_cache(maxsize=None)` which is also the default for `@lru_cache`. See **[[Functools Module in Python#`@cache` decorator|here]]**.
###### `@lru_cache` decorator from `functools`
See **[[Functools Module in Python#`@lru_cache` decorator|here]]**.