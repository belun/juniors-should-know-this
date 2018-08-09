# Concept modeling

When we are introduced to object-oriented programming \(_OOP_\), we are often \(I was\) "sold" the idea that object oriented will help us better model the world \(and thus the business logic / the processes that need to be turned into software\). 

You probably heard things like "classes are just like real-world objects, with properties / attributes and functionalities".

Let's take some real world concepts that are not so abstract : _Person_ and _Door._

### What is corect OOP?

#### Is it ok for a _Person_ to .open\(\) a _Door_?

```java
Person.open(door);
```

Sounds about right.

#### Is it ok for a _Door to be "told"_ to .open\(\) __?

```java
Door.open();
```

Um... maybe?!

