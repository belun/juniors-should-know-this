---
description: Concept definition
---

# Encapsulation

#### What is encapsulation?

Encapsulation is about keeping together all the resources needed to perform a specific functionality.

In programming, these are : data and logic. 

In object-oriented programming,

* the data is represented by the fields \(that represent that state\) of a class
* and the logic is in the methods \(the perform the desired logic\)
* the container \(that should encapsulate data and logic\) is represented by a class

#### How do I do encapsulation?

Keep the business logic in the same class as the data needed to perform that business logic. Make rich classes.

The classes that perform logic on certain data should be seen as "owners" of that data and should treat \(and hide\) this data as internal details.

Exposing internal state, so that some other classes can do logic on that data means to break encapsulation.

#### Is there a rule / guideline / principle for this?

Yes, it is called _the expert principle._

#### What do I gain if I do this?

The abstractions that respect encapsulation can be seen as a black-boxes now. This can help with composing several abstractions to build new ones \(without having to worry what are the implementation details of each composed abstraction\).

#### Here are some other good explanations

1. [Definitions of encapsulation](https://searchnetworking.techtarget.com/definition/encapsulation)
2. [OOP Concept for Beginners: What is Encapsulation](https://stackify.com/oop-concept-for-beginners-what-is-encapsulation/)

