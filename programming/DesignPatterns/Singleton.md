# Singleton
Reference: [Refactoring Guru](https://refactoring.guru/design-patterns/singleton)
Jump Back to [[_Index_|Index]]
Jump to [[Singleton#Code Examples|Code]]

---
## Intent
**Singleton** is a [[_Index_#Creational patterns|creational]] design pattern that lets you ensure that a class has only one instance, while providing a global access point to this instance.
### Problem
The Singleton pattern solves two problems at the same time, violating the _Single Responsibility Principle_:
1. **Ensure that a class has just a single instance**. Why would anyone want to control how many instances a class has? The most common reason for this is to control access to some shared resource. For example, a database or a file. Here’s how it works: imagine that you created an object, but after a while decided to create a new one. Instead of receiving a fresh object, you’ll get the one you already created. Note that this behavior is impossible to implement with a regular constructor since a constructor call **must** always return a new object by design.
2. **Provide a global access point to that instance**. Remember those global variables that you used to store some essential objects? While they’re very handy, they’re also very unsafe since any code can potentially overwrite the contents of those variables and crash the app. Just like a global variable, the Singleton pattern lets you access some object from anywhere in the program. However, it also protects that instance from being overwritten by other code. There’s another side to this problem: you don’t want the code that solves problem #1 to be scattered all over your program. It’s much better to have it within one class, especially if the rest of your code already depends on it.

Nowadays, the Singleton pattern has become so popular that people may call something a _singleton_ even if it solves just one of the listed problems.
### Solution
All implementations of the Singleton have these two steps in common:
- Make the default constructor private, to prevent other objects from using the `new` operator with the Singleton class.
- Create a static creation method that acts as a constructor. Under the hood, this method calls the private constructor to create an object and saves it in a static field. All following calls to this method return the cached object.

If your code has access to the Singleton class, then it’s able to call the Singleton’s static method. So whenever that method is called, the same object is always returned.
## Structure
![[../../Resources/Images/DP/singleton.png]]
The **Singleton** class declares the static method `getInstance` that returns the same instance of its own class. The Singleton’s constructor should be hidden from the client code. Calling the `getInstance` method should be the only way of getting the Singleton object.
### Pseudocode
```java
// The Database class defines the `getInstance` method that lets clients access the same instance of a database connection throughout the program.
class Database is
    // The field for storing the singleton instance should be static.
    private static field instance: Database

    // The singleton's constructor should always be private to prevent direct construction calls with the `new` operator.
    private constructor Database() is
        // Some initialization code, such as the actual connection to a database server.

    // The static method that controls access to the singleton instance.
    public static method getInstance() is
        if (Database.instance == null) then
            acquireThreadLock() and then
                // Ensure that the instance hasn't yet been initialized by another thread while this one has been waiting for the lock's release.
                if (Database.instance == null) then
                    Database.instance = new Database()
        return Database.instance

    // Finally, any singleton should define some business logic which can be executed on its instance.
    public method query(sql) is
        // For instance, all database queries of an app go through this method. Therefore, you can place throttling or caching logic here.

class Application is
    method main() is
        Database foo = Database.getInstance()
        foo.query("SELECT ...")
        // ...
        Database bar = Database.getInstance()
        bar.query("SELECT ...")
        // The variable `bar` will contain the same object as
        // the variable `foo`.
```

## Applicability
> [!bug] Use the Singleton pattern when a class in your program should have just a single instance available to all clients; for example, a single database object shared by different parts of the program.
> The Singleton pattern disables all other means of creating objects of a class except for the special creation method. This method either creates a new object or returns an existing one if it has already been created.

> [!bug] Use the Singleton pattern when you need stricter control over global variables.
> Unlike global variables, the Singleton pattern guarantees that there’s just one instance of a class. Nothing, except for the Singleton class itself, can replace the cached instance.
> 
> Note that you can always adjust this limitation and allow creating any number of Singleton instances. The only piece of code that needs changing is the body of the `getInstance` method.

### How to Implement
1. Add a private static field to the class for storing the singleton instance.
2. Declare a public static creation method for getting the singleton instance.
3. Implement “lazy initialization” inside the static method. It should create a new object on its first call and put it into the static field. The method should always return that instance on all subsequent calls.
4. Make the constructor of the class private. The static method of the class will still be able to call the constructor, but not the other objects.
5. Go over the client code and replace all direct calls to the singleton’s constructor with calls to its static creation method.

#### Pros
- You can be sure that a class has only a single instance.
- You gain a global access point to that instance.
- The singleton object is initialized only when it’s requested for the first time.

#### Cons
- Violates the _Single Responsibility Principle_. The pattern solves two problems at the time.
- The Singleton pattern can mask bad design, for instance, when the components of the program know too much about each other.
- The pattern requires special treatment in a multithreaded environment so that multiple threads won’t create a singleton object several times.
- It may be difficult to unit test the client code of the Singleton because many test frameworks rely on inheritance when producing mock objects. Since the constructor of the singleton class is private and overriding static methods is impossible in most languages, you will need to think of a creative way to mock the singleton. Or just don’t write the tests. Or don’t use the Singleton pattern.

## Relation with Other Patterns
- A [[Facade]] class can often be transformed into a [[Singleton]] since a single facade object is sufficient in most cases.
    
- [[Flyweight]] would resemble [[Singleton]] if you somehow managed to reduce all shared states of the objects to just one flyweight object. But there are two fundamental differences between these patterns:
    
    1. There should be only one Singleton instance, whereas a _Flyweight_ class can have multiple instances with different intrinsic states.
    2. The _Singleton_ object can be mutable. Flyweight objects are immutable.
- [[Abstract Factories]], [[Builders]] and [[Prototypes]] can all be implemented as [[Singleton|Singletons]].

# Code Examples
**Complexity:**  🌟 ⭐ ⭐
**Popularity:** 🌟 🌟 ⭐

**Usage examples:** A lot of developers consider the Singleton pattern an anti-pattern. That’s why its usage is on the decline in code.

**Identification:** Singleton can be recognized by a static creation method, which returns the same cached object.
### C++
It’s pretty easy to implement a sloppy Singleton. You just need to hide the constructor and implement a static creation method.
> [!error] The same class behaves incorrectly in a multi-threaded environment. Multiple threads can call the creation method simultaneously and get several instances of Singleton class.
> To fix the problem, you have to synchronize threads during the first creation of the Singleton object.
> For that implementation look [here](https://refactoring.guru/design-patterns/singleton/cpp/example#example-1)
##### naiveSingleton.cc 
```cpp
// The Singleton class defines the `GetInstance` method that serves as an alternative to constructor and lets clients access the same instance of this class over and over.
class Singleton
{
    // The Singleton's constructor should always be private to prevent direct construction calls with the `new` operator.
protected:
    Singleton(const std::string value): value_(value)
    {
    }
    static Singleton* singleton_;
    std::string value_;
public:
     // Singletons should not be cloneable.
    Singleton(Singleton &other) = delete;
     // Singletons should not be assignable.
    void operator=(const Singleton &) = delete;
     
     // This is the static method that controls the access to the singleton instance. On the first run, it creates a singleton object and places it into the static field. On subsequent runs, it returns the client existing object stored in the static field.
    static Singleton *GetInstance(const std::string& value);

    void SomeBusinessLogic(){}
    
    std::string value() const{
        return value_;
    } 
};

Singleton* Singleton::singleton_= nullptr;;
 // Static methods should be defined outside the class.

Singleton *Singleton::GetInstance(const std::string& value)
{
	 // This is a safer way to create an instance. instance = new Singleton is dangeruous in case two instance threads wants to access at the same time
    if(singleton_==nullptr){
        singleton_ = new Singleton(value);
    }
    return singleton_;
}

void ThreadFoo(){
    // Following code emulates slow initialization.
    std::this_thread::sleep_for(std::chrono::milliseconds(1000));
    Singleton* singleton = Singleton::GetInstance("FOO");
    std::cout << singleton->value() << "\n";
}

void ThreadBar(){
    // Following code emulates slow initialization.
    std::this_thread::sleep_for(std::chrono::milliseconds(1000));
    Singleton* singleton = Singleton::GetInstance("BAR");
    std::cout << singleton->value() << "\n";
}

int main()
{
    std::cout <<"If you see the same value, then singleton was reused (yay!\n" <<
                "If you see different values, then 2 singletons were created (booo!!)\n\n" <<
                "RESULT:\n";   
    std::thread t1(ThreadFoo);
    std::thread t2(ThreadBar);
    t1.join();
    t2.join();
    return 0;
}
```
###### Execution Result
```
If you see the same value, then singleton was reused (yay!
If you see different values, then 2 singletons were created (booo!!)

RESULT:
BAR
FOO
```
### Java
 **Java Library Usage:**
 - [`java.lang.Runtime#getRuntime()`](http://docs.oracle.com/javase/8/docs/api/java/lang/Runtime.html#getRuntime--)
- [`java.awt.Desktop#getDesktop()`](http://docs.oracle.com/javase/8/docs/api/java/awt/Desktop.html#getDesktop--)
- [`java.lang.System#getSecurityManager()`](http://docs.oracle.com/javase/8/docs/api/java/lang/System.html#getSecurityManager--)

It’s pretty easy to implement a sloppy Singleton. You just need to hide the constructor and implement a static creation method.
#### Singleton.java
It’s pretty easy to implement a sloppy Singleton. You just need to hide the constructor and implement a static creation method.
```java
public final class Singleton {
    private static Singleton instance;
    public String value;

    private Singleton(String value) {
        // The following code emulates slow initialization.
        try {
            Thread.sleep(1000);
        } catch (InterruptedException ex) {
            ex.printStackTrace();
        }
        this.value = value;
    }

    public static Singleton getInstance(String value) {
        if (instance == null) {
            instance = new Singleton(value);
        }
        return instance;
    }
}
```
> [!error] The same class behaves incorrectly in a multi-threaded environment. Multiple threads can call the creation method simultaneously and get several instances of Singleton class.
> To fix the problem, you have to synchronize threads during first creation of the Singleton object.
> ```java
> public final class Singleton {
>     // The field must be declared volatile so that double check lock would work correctly.
>     private static volatile Singleton instance;
> 
>     public String value;
> 
>     private Singleton(String value) {
>         this.value = value;
>     }
> 
>     public static Singleton getInstance(String value) {
>         // The approach taken here is called double-checked locking (DCL). It exists to prevent race condition between multiple threads that may to get singleton instance at the same time, creating separate instances as a result.
>
>         // It may seem that having the `result` variable here is completely// pointless. There is, however, a very important caveat when implementing double-checked locking in Java, which is solved by introducing this local variable.
>         
>         // You can read more info DCL issues in Java here:
>         // https://refactoring.guru/java-dcl-issue
>         Singleton result = instance;
>         if (result != null) {
>             return result;
>         }
>         synchronized(Singleton.class) {
>             if (instance == null) {
>                 instance = new Singleton(value);
>             }
>             return instance;
>         }
>     }
> }
> ```

##### DemoSingleThread.java
```java
public class DemoSingleThread {
    public static void main(String[] args) {
        System.out.println("If you see the same value, then singleton was reused (yay!)" + "\n" +
                "If you see different values, then 2 singletons were created (booo!!)" + "\n\n" +
                "RESULT:" + "\n");
        Singleton singleton = Singleton.getInstance("FOO");
        Singleton anotherSingleton = Singleton.getInstance("BAR");
        System.out.println(singleton.value);
        System.out.println(anotherSingleton.value);
    }
}
```
###### Execution Result
```
If you see the same value, then singleton was reused (yay!)
If you see different values, then 2 singletons were created (booo!!)

RESULT:

FOO
FOO
```
##### DemoMultiThread.java
```java
public class DemoMultiThread {
    public static void main(String[] args) {
        System.out.println("If you see the same value, then singleton was reused (yay!)" + "\n" +
                "If you see different values, then 2 singletons were created (booo!!)" + "\n\n" +
                "RESULT:" + "\n");
        Thread threadFoo = new Thread(new ThreadFoo());
        Thread threadBar = new Thread(new ThreadBar());
        threadFoo.start();
        threadBar.start();
    }

    static class ThreadFoo implements Runnable {
        @Override
        public void run() {
            Singleton singleton = Singleton.getInstance("FOO");
            System.out.println(singleton.value);
        }
    }

    static class ThreadBar implements Runnable {
        @Override
        public void run() {
            Singleton singleton = Singleton.getInstance("BAR");
            System.out.println(singleton.value);
        }
    }
}
```
###### Execution Result
```
If you see the same value, then singleton was reused (yay!)
If you see different values, then 2 singletons were created (booo!!)

RESULT:

BAR
BAR
```
### Python
It’s pretty easy to implement a sloppy Singleton. You just need to hide the constructor and implement a static creation method.
> [!error] The same class behaves incorrectly in a multi-threaded environment. Multiple threads can call the creation method simultaneously and get several instances of Singleton class.
> To fix the problem, you have to synchronize threads during the first creation of the Singleton object.
> For that implementation look [here](https://refactoring.guru/design-patterns/singleton/python/example#example-1)
##### naiveSingleton.py
```python
class SingletonMeta(type):
    """
    The Singleton class can be implemented in different ways in Python. Some possible methods include: base class, decorator, metaclass. We will use the metaclass because it is best suited for this purpose.
    """
    _instances = {}

    def __call__(cls, *args, **kwargs):
        """
        Possible changes to the value of the `__init__` argument do not affect the returned instance.
        """
        if cls not in cls._instances:
            instance = super().__call__(*args, **kwargs)
            cls._instances[cls] = instance
        return cls._instances[cls]

class Singleton(metaclass=SingletonMeta):
    def some_business_logic(self):
        """
        Finally, any singleton should define some business logic, which can be executed on its instance.
        """

if __name__ == "__main__":
    # The client code.

    s1 = Singleton()
    s2 = Singleton()

    if id(s1) == id(s2):
        print("Singleton works, both variables contain the same instance.")
    else:
        print("Singleton failed, variables contain different instances.")
```
###### Execution Result
```
Singleton works, both variables contain the same instance.
```