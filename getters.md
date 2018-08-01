---
description: Why / how and when to use them
---

# Getters

Notice how in the "transferring data" section, there was no mention of "exposing data" \(as in, make use of getters\). 

That is because Getters can lead to breaking of encapsulation.

#### What if I need to expose data?

Surely, data might need to be "exposed" for presentation \(or even for persistence\). And in this case, use Getters. 

Or, even more straight forward, expose directly the fields of the class.

A more elegant _way_ would be to create _data transfer objects_ \(DTOs ; objects that do not perform logic\). This, however, adds a new layer of abstraction.

#### What if I do not want extra objects \(DTOs\), but would still like to avoid Getters?

You can make use of interfaces. 

The most straight forward way would be to have **interfaces with setters** \(that accept data\) and let the classes the need that data implement those interfaces.

\(This would still respect the principle : _Tell, don't ask_\)

Note that setters do not have to receive a single piece of data. A setter can receive more that one piece of data \(more than one parameter\).

_This approach also adds another layer of abstraction._

#### So, are Getters are bad?

Not necessarily, but they can easily lead to breaking the encapsulation of classes, as the caller can start doing logic on the data collected.

{% hint style="info" %}
Keep an eye on the caller of the getters. 
{% endhint %}

#### When \(or what for\) can I use Getters?

Getters can be used for data transfer to other layers of the application \(other than the business layer, that should perform the business logic\) that do not do logic on it \(or that do logic that is purely specific for that layer ; e.g. presentation logic in presentation classes\). 

Bad code steals data from its owner and does logic on that data \(that is otherwise meant to be done by the owner\). 

This is a bad practice, as a reader might not expect \(and should not expect\) to find logic scattered all over the place.

#### What are some guidelines I can use?

Make sure that :

* no logic is done in one layer that is not part of that layer \(e.g. presentation logic in presentation layer and business logic in business layer\)
* within one layer, the data owners are clear \(rich classes contain the logic together with data, properly guard that data and do proper transfer of it\)



