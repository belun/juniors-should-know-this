---
description: Introduction of architecture concept
---

# Layers

### What are layers?

The concept of a layer refer to splitting the classes in our application in some kind of modules, and keeping the classes that do similar things together.

Just like we want to keep together, in the same class, the methods that work with common data, the expert principle can be scaled up at the architecture level.

### What layers are there?

* domain layer \(or logic layer\) : contains the low level business logic into domain classes
* application layer \(service layer\) : puts together several domains from the domain layer to provide a higher level functionality
* presentation layer
* persistance layer \(loading, saving data, etc.\) : act as wrapper to database / file-system access 
* external service layer \(or information layer\) : for accessing functionality from other applications
* provider layer : for providing functionality to other applications

### How can you tell what layer you are in?

{% hint style="info" %}
Whenever writing a class, look at the imports of that class to determine its layer.
{% endhint %}

If the class imports only other domain classes \(classes with business logic\), then that class is part of the domain layer.

If the class depends on classes that deal with database access,  then that class is database \(persistence\) layer.

Etc.

### Why layers?

Having layers in our architecture \(splitting the application in some kind of architectural components\) could help with maintaining our application.

Consider classes to be containers of logic \(while hiding the detail as an abstraction\), while layers are containers of abstractions. 

#### Some remarks about architecture

_The purpose of introducing the concept of layers was to make you aware that the concepts of encapsulation, cohesion, good abstraction apply not only at the lowest level \(the class level or domain level\), but also higher level \(packages, layers, modules\)._

