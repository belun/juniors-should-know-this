---
description: How to transfer data
---

# Moving state around

**Given** _rich classes_, that are "owners" of data, 

and _trying to not break encapsulation_ \(by avoiding expose internal state, so that some other classes can do logic on that data\)

#### What happens when I need to transfer data to another class?

It can happen that certain data can be used to perform several pieces of logic \(which are not all placed in the same class\), what do I do then? Should I put all logic in one huge class?

This could be a potential solution, however, the cohesion of that class would be very  low.

#### How do I maintain encapsulation and have a good cohesion?

Transfer data to another class \(and,of course, transfer only what data is needed\)

Data transfer can be done by :

* either creating a new instance of a class \(and pass the data in its constructor\)
  * sometimes, however, several classes \(data owners\) must participate in transferring data to the same destination, and for this, the Builder pattern can be used to collect data before instantiating the new class
* or, calling the method that performs the logic that needs that piece of data in the first place, and pass the data as parameter

#### Is there a more generic guideline / rule or principle for all of this?

Yes, it is. [_Tell, don't ask_](https://martinfowler.com/bliki/TellDontAsk.html)_._



