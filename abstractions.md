---
description: Concept definition
---

# Abstraction\(s\)

#### How can the code help the maintainers ?

The answer is : [_abstractions_](https://whatis.techtarget.com/definition/abstraction). 

The code can help by hiding the details of the logic that it performs, while presenting only the relevant essentials. 

#### How does this help?

Hiding the details improves the expressiveness of the logic that the code implements. It makes life easier for reader.

#### What is the trick?

The important thing to keep in mind, once an abstraction is put in place, is the name given to the abstraction. 

Misleading names or irrelevant names forces the maintainer to go into the abstraction to see what it does. This adds extra work for the reader.

#### How to come up with proper names?

_The name of an abstraction should express what that abstraction does_. 

Look at the internal state of the abstraction \(the fields that a class has\) and the functionality it can perform \(the public methods that a class exposes\) and name the abstraction according to what you see inside. A good name helps the reader by not having to go inside the abstraction later.

Very often, we name pieces of code for the place they are meant to used, instead of what the code does.

#### How do I do this as developer?

_How do I setup good abstractions?_

Make use of _encapsulation_. Together with _abstractions_ \(and _inheritance_\), _encapsulation_ is one of the core principles of object-oriented programming.

{% hint style="info" %}
If you program in an object-oriented language \(or a language that support object-oriented programming\), then you should make use of its core principles \(and use them properly\).
{% endhint %}

