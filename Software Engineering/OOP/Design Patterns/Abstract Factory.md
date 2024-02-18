# Abstract Factory
Reference: [Refactoring Guru](https://refactoring.guru/design-patterns/abstract-factory)
Read More on [Factory Comaprison](https://refactoring.guru/design-patterns/factory-comparison)
Jump Back to [[_Index_|Index]]
Jump to [[Abstract Factory#Code Examples|Code]]

---
## Intent
**Abstract Factory** is a [[_Index_#Creational patterns|creational]] design pattern that lets you produce families of related objects without specifying their concrete classes.
### Problem
Imagine that you’re creating a furniture shop simulator. Your code consists of classes that represent:
1. A family of related products, say: `Chair` + `Sofa` + `CoffeeTable`.
2. Several variants of this family. For example, products `Chair` + `Sofa` + `CoffeeTable` are available in these variants: `Modern`, `Victorian`, `ArtDeco`.

You need a way to create individual furniture objects so that they match other objects of the same family. Customers get quite mad when they receive non-matching furniture.
Also, you don’t want to change existing code when adding new products or families of products to the program. Furniture vendors update their catalogs very often, and you wouldn’t want to change the core code each time it happens.
### Solution
The first thing the Abstract Factory pattern suggests is to explicitly declare interfaces for each distinct product of the product family (e.g., chair, sofa or coffee table). Then you can make all variants of products follow those interfaces. For example, all chair variants can implement the `Chair` interface; all coffee table variants can implement the `CoffeeTable` interface, and so on.

The next move is to declare the _Abstract Factory_—an interface with a list of creation methods for all products that are part of the product family (for example, `createChair`, `createSofa` and `createCoffeeTable`). These methods must return **abstract** product types represented by the interfaces we extracted previously: `Chair`, `Sofa`, `CoffeeTable` and so on.

Now, how about the product variants? For each variant of a product family, we create a separate factory class based on the `AbstractFactory` interface. A factory is a class that returns products of a particular kind. For example, the `ModernFurnitureFactory` can only create `ModernChair`, `ModernSofa` and `ModernCoffeeTable` objects.

The client code has to work with both factories and products via their respective abstract interfaces. This lets you change the type of a factory that you pass to the client code, as well as the product variant that the client code receives, without breaking the actual client code.

Say the client wants a factory to produce a chair. The client doesn’t have to be aware of the factory’s class, nor does it matter what kind of chair it gets. Whether it’s a Modern model or a Victorian-style chair, the client must treat all chairs in the same manner, using the abstract `Chair` interface. With this approach, the only thing that the client knows about the chair is that it implements the `sitOn` method in some way. Also, whichever variant of the chair is returned, it’ll always match the type of sofa or coffee table produced by the same factory object.

There’s one more thing left to clarify: if the client is only exposed to the abstract interfaces, what creates the actual factory objects? Usually, the application creates a concrete factory object at the initialization stage. Just before that, the app must select the factory type depending on the configuration or the environment settings.
## Structure
![[../../../Resources/Images/DP/abstract-factory.png]]
1. **Abstract Products** declare interfaces for a set of distinct but related products which make up a product family.
2. **Concrete Products** are various implementations of abstract products, grouped by variants. Each abstract product (chair/sofa) must be implemented in all given variants (Victorian/Modern).
3. The **Abstract Factory** interface declares a set of methods for creating each of the abstract products.
4. **Concrete Factories** implement creation methods of the abstract factory. Each concrete factory corresponds to a specific variant of products and creates only those product variants.
5. Although concrete factories instantiate concrete products, signatures of their creation methods must return corresponding _abstract_ products. This way the client code that uses a factory doesn’t get coupled to the specific variant of the product it gets from a factory. The **Client** can work with any concrete factory/product variant, as long as it communicates with their objects via abstract interfaces.
### Pseudocode
This example illustrates how the **Abstract Factory** pattern can be used for creating cross-platform UI elements without coupling the client code to concrete UI classes, while keeping all created elements consistent with a selected operating system.

The same UI elements in a cross-platform application are expected to behave similarly, but look a little bit different under different operating systems. Moreover, it’s your job to make sure that the UI elements match the style of the current operating system. You wouldn’t want your program to render macOS controls when it’s executed in Windows.

The Abstract Factory interface declares a set of creation methods that the client code can use to produce different types of UI elements. Concrete factories correspond to specific operating systems and create the UI elements that match that particular OS.

It works like this: when an application launches, it checks the type of the current operating system. The app uses this information to create a factory object from a class that matches the operating system. The rest of the code uses this factory to create UI elements. This prevents the wrong elements from being created.

With this approach, the client code doesn’t depend on concrete classes of factories and UI elements as long as it works with these objects via their abstract interfaces. This also lets the client code support other factories or UI elements that you might add in the future.

As a result, you don’t need to modify the client code each time you add a new variation of UI elements to your app. You just have to create a new factory class that produces these elements and slightly modify the app’s initialization code so it selects that class when appropriate.
```java
// The abstract factory interface declares a set of methods that return different abstract products. These products are called a family and are related by a high-level theme or concept.

// Products of one family are usually able to collaborate among themselves. A family of products may have several variants, but the products of one variant are incompatible with the products of another variant.

interface GUIFactory is
    method createButton():Button
    method createCheckbox():Checkbox

// Concrete factories produce a family of products that belong to a single variant. The factory guarantees that the resulting products are compatible. Signatures of the concrete factory's methods return an abstract product, while inside the method a concrete product is instantiated.
class WinFactory implements GUIFactory is
    method createButton():Button is
        return new WinButton()
    method createCheckbox():Checkbox is
        return new WinCheckbox()

// Each concrete factory has a corresponding product variant.
class MacFactory implements GUIFactory is
    method createButton():Button is
        return new MacButton()
    method createCheckbox():Checkbox is
        return new MacCheckbox()

// Each distinct product of a product family should have a base interface. All variants of the product must implement this interface.
interface Button is
    method paint()

// Concrete products are created by corresponding concrete factories.
class WinButton implements Button is
    method paint() is
        // Render a button in Windows style.

class MacButton implements Button is
    method paint() is
        // Render a button in macOS style.

// Here's the base interface of another product. All products can interact with each other, but proper interaction is possible only between products of the same concrete variant.
interface Checkbox is
    method paint()

class WinCheckbox implements Checkbox is
    method paint() is
        // Render a checkbox in Windows style.

class MacCheckbox implements Checkbox is
    method paint() is
        // Render a checkbox in macOS style.

// The client code works with factories and products only through abstract types: GUIFactory, Button and Checkbox. This lets you pass any factory or product subclass to the client code without breaking it.
class Application is
    private field factory: GUIFactory
    private field button: Button
    constructor Application(factory: GUIFactory) is
        this.factory = factory
    method createUI() is
        this.button = factory.createButton()
    method paint() is
        button.paint()

// The application picks the factory type depending on the current configuration or environment settings and creates it at runtime (usually at the initialization stage).
class ApplicationConfigurator is
    method main() is
        config = readApplicationConfigFile()

        if (config.OS == "Windows") then
            factory = new WinFactory()
        else if (config.OS == "Mac") then
            factory = new MacFactory()
        else
            throw new Exception("Error! Unknown operating system.")

        Application app = new Application(factory)
```

## Applicability
> [!bug] Use the Abstract Factory when your code needs to work with various families of related products, but you don’t want it to depend on the concrete classes of those products—they might be unknown beforehand or you simply want to allow for future extensibility.
> The Abstract Factory provides you with an interface for creating objects from each class of the product family. As long as your code creates objects via this interface, you don’t have to worry about creating the wrong variant of a product which doesn’t match the products already created by your app.

> [!bug] Consider implementing the Abstract Factory when you have a class with a set of [[Factory Method]] that blur its primary responsibility.
> In a well-designed program _each class is responsible only for one thing_. When a class deals with multiple product types, it may be worth extracting its factory methods into a stand-alone factory class or a full-blown Abstract Factory implementation.
### How to Implement
1. Map out a matrix of distinct product types versus variants of these products.
2. Declare abstract product interfaces for all product types. Then make all concrete product classes implement these interfaces.
3. Declare the abstract factory interface with a set of creation methods for all abstract products.
4. Implement a set of concrete factory classes, one for each product variant.
5. Create factory initialization code somewhere in the app. It should instantiate one of the concrete factory classes, depending on the application configuration or the current environment. Pass this factory object to all classes that construct products.
6. Scan through the code and find all direct calls to product constructors. Replace them with calls to the appropriate creation method on the factory object.

#### Pros
- You can be sure that the products you’re getting from a factory are compatible with each other.
- You avoid tight coupling between concrete products and client code.
- [[../S.O.L.I.D Principles#Single Responsibility|Single Responsibility Principle]]. You can extract the product creation code into one place, making the code easier to support.
- [[../S.O.L.I.D Principles#Open/closed|Open/Closed Principle]]. You can introduce new variants of products without breaking existing client code.
#### Cons
- The code may become more complicated than it should be, since a lot of new interfaces and classes are introduced along with the pattern.

## Relation with Other Patterns
- Many designs start by using [[Factory Method]] (less complicated and more customizable via subclasses) and evolve toward [[Abstract Factory]], [[Prototype]], or [[Builder]] (more flexible, but more complicated).
- [[Builder]] focuses on constructing complex objects step by step. [[Abstract Factory]] specializes in creating families of related objects. _Abstract Factory_ returns the product immediately, whereas _Builder_ lets you run some additional construction steps before fetching the product.
- [[Abstract Factory]] classes are often based on a set of [[Factory Method|Factory Methods]], but you can also use [[Prototype|Prototypes]] to compose the methods on these classes.
- [[Abstract Factory]] can serve as an alternative to [[Facade]] when you only want to hide the way the subsystem objects are created from the client code.
- You can use [[Abstract Factory]] along with [[Bridge]]. This pairing is useful when some abstractions defined by _Bridge_ can only work with specific implementations. In this case, _Abstract Factory_ can encapsulate these relations and hide the complexity from the client code.
- [[Abstract Factory|Abstract Factories]], [[Builder|Builders]] and [[Prototype|Prototypes]] can all be implemented as [[Singleton]].

# Code Examples
Abstract Factory defines an interface for creating all distinct products but leaves the actual product creation to concrete factory classes. Each factory type corresponds to a certain product variety.

The client code calls the creation methods of a factory object instead of creating products directly with a constructor call (`new` operator). Since a factory corresponds to a single product variant, all its products will be compatible.

Client code works with factories and products only through their abstract interfaces. This lets the client code work with any product variants, created by the factory object. You just create a new concrete factory class and pass it to the client code.

**Complexity:**  🌟 🌟 ⭐
**Popularity:** 🌟 🌟 🌟

**Usage examples:** The Abstract Factory pattern is pretty common in code. Many frameworks and libraries use it to provide a way to extend and customize their standard components.

**Identification:** The pattern is easy to recognize by methods, which return a factory object. Then, the factory is used for creating specific sub-components.
### C++
##### abstractFactory.cc
```cpp
// Each distinct product of a product family should have a base interface. All variants of the product must implement this interface.
class AbstractProductA {
 public:
  virtual ~AbstractProductA(){};
  virtual std::string UsefulFunctionA() const = 0;
};

// Concrete Products are created by corresponding Concrete Factories.
class ConcreteProductA1 : public AbstractProductA {
 public:
  std::string UsefulFunctionA() const override {
    return "The result of the product A1.";
  }
};

class ConcreteProductA2 : public AbstractProductA {
  std::string UsefulFunctionA() const override {
    return "The result of the product A2.";
  }
};

// Here's the the base interface of another product. All products can interact with each other, but proper interaction is possible only between products of the same concrete variant.
class AbstractProductB {
  // Product B is able to do its own thing...
 public:
  virtual ~AbstractProductB(){};
  virtual std::string UsefulFunctionB() const = 0;
  // ...but it also can collaborate with the ProductA.
  
  // The Abstract Factory makes sure that all products it creates are of the same variant and thus, compatible.
  virtual std::string AnotherUsefulFunctionB(const AbstractProductA &collaborator) const = 0;
};

// Concrete Products are created by corresponding Concrete Factories.
class ConcreteProductB1 : public AbstractProductB {
 public:
  std::string UsefulFunctionB() const override {
    return "The result of the product B1.";
  }
  
  // The variant, Product B1, is only able to work correctly with the variant, Product A1. Nevertheless, it accepts any instance of AbstractProductA as an argument.
  std::string AnotherUsefulFunctionB(const AbstractProductA &collaborator) const override {
    const std::string result = collaborator.UsefulFunctionA();
    return "The result of the B1 collaborating with ( " + result + " )";
  }
};

class ConcreteProductB2 : public AbstractProductB {
 public:
  std::string UsefulFunctionB() const override {
    return "The result of the product B2.";
  }
  
  // The variant, Product B2, is only able to work correctly with the variant, Product A2. Nevertheless, it accepts any instance of AbstractProductA as an argument.
  std::string AnotherUsefulFunctionB(const AbstractProductA &collaborator) const override {
    const std::string result = collaborator.UsefulFunctionA();
    return "The result of the B2 collaborating with ( " + result + " )";
  }
};

// The Abstract Factory interface declares a set of methods that return different abstract products. These products are called a family and are related by a high-level theme or concept. 
// Products of one family are usually able to collaborate among themselves. A family of products may have several variants, but the products of one variant are incompatible with products of another.
class AbstractFactory {
 public:
  virtual AbstractProductA *CreateProductA() const = 0;
  virtual AbstractProductB *CreateProductB() const = 0;
};

// Concrete Factories produce a family of products that belong to a single variant. The factory guarantees that resulting products are compatible. Note that signatures of the Concrete Factory's methods return an abstract product, while inside the method a concrete product is instantiated.
class ConcreteFactory1 : public AbstractFactory {
 public:
  AbstractProductA *CreateProductA() const override {
    return new ConcreteProductA1();
  }
  AbstractProductB *CreateProductB() const override {
    return new ConcreteProductB1();
  }
};

// Each Concrete Factory has a corresponding product variant.
class ConcreteFactory2 : public AbstractFactory {
 public:
  AbstractProductA *CreateProductA() const override {
    return new ConcreteProductA2();
  }
  AbstractProductB *CreateProductB() const override {
    return new ConcreteProductB2();
  }
};

// The client code works with factories and products only through abstract types: AbstractFactory and AbstractProduct. This lets you pass any factory or product subclass to the client code without breaking it.
void ClientCode(const AbstractFactory &factory) {
  const AbstractProductA *product_a = factory.CreateProductA();
  const AbstractProductB *product_b = factory.CreateProductB();
  std::cout << product_b->UsefulFunctionB() << "\n";
  std::cout << product_b->AnotherUsefulFunctionB(*product_a) << "\n";
  delete product_a;
  delete product_b;
}

int main() {
  std::cout << "Client: Testing client code with the first factory type:\n";
  ConcreteFactory1 *f1 = new ConcreteFactory1();
  ClientCode(*f1);
  delete f1;
  std::cout << std::endl;
  std::cout << "Client: Testing the same client code with the second factory type:\n";
  ConcreteFactory2 *f2 = new ConcreteFactory2();
  ClientCode(*f2);
  delete f2;
  return 0;
}
```
###### Execution Result
```
Client: Testing client code with the first factory type:
The result of the product B1.
The result of the B1 collaborating with the (The result of the product A1.)

Client: Testing the same client code with the second factory type:
The result of the product B2.
The result of the B2 collaborating with the (The result of the product A2.)
```
### Java
 **Java Library Usage:**
 - [`javax.xml.parsers.DocumentBuilderFactory#newInstance()`](http://docs.oracle.com/javase/8/docs/api/javax/xml/parsers/DocumentBuilderFactory.html#newInstance--)
- [`javax.xml.transform.TransformerFactory#newInstance()`](http://docs.oracle.com/javase/8/docs/api/javax/xml/transform/TransformerFactory.html#newInstance--)
- [`javax.xml.xpath.XPathFactory#newInstance()`](http://docs.oracle.com/javase/8/docs/api/javax/xml/xpath/XPathFactory.html#newInstance--)
---
In this example, buttons and checkboxes will act as products. They have two variants: macOS and Windows.

The abstract factory defines an interface for creating buttons and checkboxes. There are two concrete factories, which return both products in a single variant.

Client code works with factories and products using abstract interfaces. It makes the same client code working with many product variants, depending on the type of factory object.
>[!faq] First Product Hierarchy -> `buttons/`

>[!faq] Second Product Hierarchy -> `checkboxes/`

##### buttons/Button.java
```java
package buttons;
// Abstract Factory assumes that you have several families of products, structured into separate class hierarchies (Button/Checkbox). All products of the same family have the common interface.

 // This is the common interface for buttons family.
 public interface Button {
    void paint();
}
```
##### buttons/MacOSButton.java
```java
package buttons;
// All products families have the same varieties (MacOS/Windows).

public class MacOSButton implements Button {
    @Override
    public void paint() {
        System.out.println("You have created MacOSButton.");
    }
}
```
##### buttons/WindowsButton.java
```java
package buttons;
// All products families have the same varieties (MacOS/Windows).

public class WindowsButton implements Button {
    @Override
    public void paint() {
        System.out.println("You have created WindowsButton.");
    }
}
```
##### checkboxes/Checkbox.java
```java
package checkboxes;
// Checkboxes is the second product family. It has the same variants as buttons.
public interface Checkbox {
    void paint();
}
```
##### checkboxes/MacOSCheckbox.java
```java
package checkboxes;
// All products families have the same varieties (MacOS/Windows).

public class MacOSCheckbox implements Checkbox {
    @Override
    public void paint() {
        System.out.println("You have created MacOSCheckbox.");
    }
}
```
##### checkboxes/WindowsCheckbox.java
```java
package checkboxes;
// All products families have the same varieties (MacOS/Windows).

// This is another variant of a button.
public class WindowsCheckbox implements Checkbox {
    @Override
    public void paint() {
        System.out.println("You have created WindowsCheckbox.");
    }
}
```
##### factories/GUIFactory.java (Abstract factory)
```java
package factories;
import buttons.Button;
import checkboxes.Checkbox;
// Abstract factory knows about all (abstract) product types.

public interface GUIFactory {
    Button createButton();
    Checkbox createCheckbox();
}
```
##### factories/MacOSFactory.java (Concrete factory)
```java
package factories;
import buttons.Button;
import buttons.MacOSButton;
import checkboxes.Checkbox;
import checkboxes.MacOSCheckbox;
// Each concrete factory extends basic factory and responsible for creating products of a single variety.

public class MacOSFactory implements GUIFactory {
    @Override
    public Button createButton() {
        return new MacOSButton();
    }
    @Override
    public Checkbox createCheckbox() {
        return new MacOSCheckbox();
    }
}
```
##### factories/WindowsFactory.java (Concrete factory)
```java
package factories;
import buttons.Button;
import buttons.WindowsButton;
import checkboxes.Checkbox;
import checkboxes.WindowsCheckbox;
// Each concrete factory extends basic factory and responsible for creating products of a single variety.

public class WindowsFactory implements GUIFactory {
    @Override
    public Button createButton() {
        return new WindowsButton();
    }
    @Override
    public Checkbox createCheckbox() {
        return new WindowsCheckbox();
    }
}
```
##### app/Application.java (Client Code)
```java
package app;

import buttons.Button;
import checkboxes.Checkbox;
import factories.GUIFactory;

// Factory users don't care which concrete factory they use since they work with factories and products through abstract interfaces.
public class Application {
    private Button button;
    private Checkbox checkbox;

    public Application(GUIFactory factory) {
        button = factory.createButton();
        checkbox = factory.createCheckbox();
    }
    public void paint() {
        button.paint();
        checkbox.paint();
    }
}
```
##### Demo.java (App Configuration)
```java
import app.Application;
import factories.GUIFactory;
import factories.MacOSFactory;
import factories.WindowsFactory;

public class Demo {
    // Application picks the factory type and creates it in run time (usually at initialization stage), depending on the configuration or environment variables.
    private static Application configureApplication() {
        Application app;
        GUIFactory factory;
        String osName = System.getProperty("os.name").toLowerCase();
        if (osName.contains("mac")) {
            factory = new MacOSFactory();
        } else {
            factory = new WindowsFactory();
        }
        app = new Application(factory);
        return app;
    }

    public static void main(String[] args) {
        Application app = configureApplication();
        app.paint();
    }
}
```
###### Execution Result
```
You create WindowsButton.
You created WindowsCheckbox.
```
### Python
##### abstractFactory.py
```python
from __future__ import annotations
from abc import ABC, abstractmethod

class AbstractFactory(ABC):
    """
    The Abstract Factory interface declares a set of methods that return different abstract products. These products are called a family and are related by a high-level theme or concept. Products of one family are usually able to collaborate among themselves. A family of products may have several variants, but the products of one variant are incompatible with products of another.
    """
    @abstractmethod
    def create_product_a(self) -> AbstractProductA:
        pass

    @abstractmethod
    def create_product_b(self) -> AbstractProductB:
        pass

class ConcreteFactory1(AbstractFactory):
    """
    Concrete Factories produce a family of products that belong to a single variant. The factory guarantees that resulting products are compatible. Note that signatures of the Concrete Factory's methods return an abstract product, while inside the method a concrete product is instantiated.
    """

    def create_product_a(self) -> AbstractProductA:
        return ConcreteProductA1()

    def create_product_b(self) -> AbstractProductB:
        return ConcreteProductB1()

class ConcreteFactory2(AbstractFactory):
    """
    Each Concrete Factory has a corresponding product variant.
    """

    def create_product_a(self) -> AbstractProductA:
        return ConcreteProductA2()

    def create_product_b(self) -> AbstractProductB:
        return ConcreteProductB2()

class AbstractProductA(ABC):
    """
    Each distinct product of a product family should have a base interface. All variants of the product must implement this interface.
    """

    @abstractmethod
    def useful_function_a(self) -> str:
        pass

"""
Concrete Products are created by corresponding Concrete Factories.
"""

class ConcreteProductA1(AbstractProductA):
    def useful_function_a(self) -> str:
        return "The result of the product A1."

class ConcreteProductA2(AbstractProductA):
    def useful_function_a(self) -> str:
        return "The result of the product A2."

class AbstractProductB(ABC):
    """
    Here's the the base interface of another product. All products can interact with each other, but proper interaction is possible only between products of the same concrete variant.
    """
    @abstractmethod
    def useful_function_b(self) -> None:
        """
        Product B is able to do its own thing...
        """
        pass

    @abstractmethod
    def another_useful_function_b(self, collaborator: AbstractProductA) -> None:
        """
        ...but it also can collaborate with the ProductA.

        The Abstract Factory makes sure that all products it creates are of the same variant and thus, compatible.
        """
        pass

"""
Concrete Products are created by corresponding Concrete Factories.
"""

class ConcreteProductB1(AbstractProductB):
    def useful_function_b(self) -> str:
        return "The result of the product B1."

    """
    The variant, Product B1, is only able to work correctly with the variant, Product A1. Nevertheless, it accepts any instance of AbstractProductA as an argument.
    """

    def another_useful_function_b(self, collaborator: AbstractProductA) -> str:
        result = collaborator.useful_function_a()
        return f"The result of the B1 collaborating with the ({result})"

class ConcreteProductB2(AbstractProductB):
    def useful_function_b(self) -> str:
        return "The result of the product B2."

    def another_useful_function_b(self, collaborator: AbstractProductA):
        """
        The variant, Product B2, is only able to work correctly with the variant, Product A2. Nevertheless, it accepts any instance of AbstractProductA as an argument.
        """
        result = collaborator.useful_function_a()
        return f"The result of the B2 collaborating with the ({result})"

def client_code(factory: AbstractFactory) -> None:
    """
    The client code works with factories and products only through abstract types: AbstractFactory and AbstractProduct. This lets you pass any factory or product subclass to the client code without breaking it.
    """
    product_a = factory.create_product_a()
    product_b = factory.create_product_b()

    print(f"{product_b.useful_function_b()}")
    print(f"{product_b.another_useful_function_b(product_a)}", end="")

if __name__ == "__main__":
    """
    The client code can work with any concrete factory class.
    """
    print("Client: Testing client code with the first factory type:")
    client_code(ConcreteFactory1())

    print("\n")

    print("Client: Testing the same client code with the second factory type:")
    client_code(ConcreteFactory2())
```
###### Execution Result
```
Client: Testing client code with the first factory type:
The result of the product B1.
The result of the B1 collaborating with the (The result of the product A1.)

Client: Testing the same client code with the second factory type:
The result of the product B2.
The result of the B2 collaborating with the (The result of the product A2.)
```