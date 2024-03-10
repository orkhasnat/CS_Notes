# [[S.O.L.I.D Principles]]
# [[Design Patterns/_Index_|Design Patterns]]

---
## *Abstract class* vs *Interface* in Java
| Abstract class                                                                              | Interface                                                                                                    |
| ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| Abstract class can **have abstract and non-abstract** methods.                              | Interface can have **only abstract** methods. Since Java 8, it can have **default and static methods** also. |
| Abstract class **doesn't support multiple inheritance**.                                    | Interface **supports multiple inheritance**.                                                                 |
| Abstract class **can have final, non-final, static and non-static variables**.              | Interface has **only static and final variables**.                                                           |
| Abstract class **can provide the implementation of interface**.                             | Interface **can't provide the implementation of abstract class**.                                            |
| The **abstract keyword** is used to declare abstract class.                                 | The **interface keyword** is used to declare interface.                                                      |
| An **abstract class** can extend another Java class and implement multiple Java interfaces. | An **interface** can extend another Java interface only.                                                     |
| An **abstract class** can be extended using keyword "extends".                              | An **interface** can be implemented using keyword "implements".                                              |
| A Java **abstract class** can have class members like private, protected, etc.              | Members of a Java interface are public by default.                                                           |
| **Example:**  <br>public abstract class Shape{  <br>public abstract void draw();  }         | **Example:**  <br>public interface Drawable{  <br>void draw();  }                                            |
## Association
Association is a relation between two separate classes which establishes through their Objects. Association can be one-to-one, one-to-many, many-to-one, many-to-many. In Object-Oriented programming, an Object communicates to another object to use functionality and services provided by that object. **Composition** and **Aggregation** are the two forms of association.
#### Composition
**Composition** is a method of wrapping the simple objects or data types into a single unit. It is a type of association used to represent the **'Part-Of'** relationship between two classes. Composition is considered as a strong association type. This is because, in composition, the parent owns the child entity, so the child entity cannot exist without its parent entity. Thus, in composition, the child entity does not have its own life cycle. We cannot directly or independently access a child entity. In the UML diagram, *composition is denoted by a filled diamond.*
> [!summary]
> Object A consists of objects B.
> A manages life cycle of B.  **B *can’t live* without A.**
#### Aggregation
**Aggregation** is another type of association that is used to represent the relationship between two classes. Aggregation is different from an ordinary composition because it gives information about a collection, and not about a mixture. Aggregation does not imply any ownership on the child entity. In aggregation, the parent and the child entities maintain **'Has-A'** relationship but both can also exist independently. We can use the parent and child entities independently. Any modification in the parent entity will not impact the child entity or vice versa. In the UML diagram, *aggregation is denoted by an empty diamond*, which shows their obvious difference in terms of strength of the relationship.
> [!summary]
> Object A contains objects B. 
> **B *can live* without A.** 
##### Difference between Composition and Aggregation
| Key          | Composition                                                                   | Aggregation                                                                        |
| ------------ | ----------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| Basic        | Composition is a way to wrap simple objects or data types into a single unit. | Aggregation differs from ordinary composition in that it does not imply ownership. |
| Relationship | In composition, parent entity owns child entity.                              | In Aggregation, parent Has-A relationship with child entity.                       |
| Tells about  | Composition tells about a mixture.                                            | Aggregation tells about a collection.                                              |
| UML Notation | It is denoted by a filled diamond.                                            | It is denoted by an empty diamond.                                                 |
| Life cycle   | Child doesn't have their own life time.                                       | Child can have their own life time.                                                |
| Association  | It is a strong association.                                                   | It is a weak association.                                                          |
## Inheritance
#### Multiple Inheritance
##### Diamond Inheritance Problem

---
# Design Principles
### Favor Composition over Inheritance
Classes should achieve polymorphic behavior and code reuse by their composition rather than inheritance from a base or parent class. To get the higher design flexibility, the design principle says that composition should be favored over inheritance.

Inheritance should *only be used when subclass **'is a'** superclass.* Don’t use inheritance to get code reuse. If there is no ‘is a’ relationship, then use composition for code reuse.
###### Reasons to Favour Composition over Inheritance
1. The fact that Java does not support multiple inheritances is one reason for favoring composition over inheritance in Java. Since you can only extend one class in Java, but if you need multiple features, such as reading and writing character data into a file, you need Reader and Writer functionality. It makes your job simple to have them as private members, and this is called Composition.
2. Composition offers better test-ability of a class than Inheritance. If one class consists of another class, you can easily construct a Mock Object representing a composed class for the sake of testing. This privilege is not given by inheritance.
3. Although both Composition and Inheritance allow you to reuse code, one of Inheritance’s disadvantages is that it breaks encapsulation. If the subclass depends on the action of the superclass for its function, it suddenly becomes fragile. When super-class behavior changes, sub-class functionality can be broken without any modification on its part.
4. In the timeless classic Design Patterns, several object-oriented design patterns listed by Gang of Four: Elements of Reusable Object-Oriented Software, favor Composition over Inheritance. Strategy design pattern, where composition and delegation are used to modify the behavior of Context without touching context code, is a classical example of this. Instead of getting it by inheritance, because Context uses composition to carry strategy, it is simple to have a new implementation of strategy at run-time.
5. Another reason why composition is preferred over inheritance is flexibility. If you use Composition, you are flexible enough to replace the better and updated version of the Composed class implementation. One example is the use of the comparator class, which provides features for comparison.