# Composition

### How to use composition?

Going back to the _Door_ implementation :

{% code-tabs %}
{% code-tabs-item title="this particular implementation has repetive \"ifs\" \(and needs cleanup\)" %}
```java
class Door {
    private final OpeningMechanism openingMechanism;    
    public Door(OpeningMechanism openingMechanism) {
        this.openingMechanism = openingMechanism;
    }
    
    public void open(OpeningDirection openingDirection) {
        if(openingDirection == OpeningDirection.INSIDE &&
            openingMechanism != OpeningMechanism.INSIDE) {
            
            throw new BrokenDoorException("Damn!! You strong.");
        }
        ...
        
        switch(openingMechanism) {
            case OpeningMechanism.INSIDE :
                openOnTheInside();
                break;
            }
            ...
    }    
    private void openOnTheInside() {
        ...
    }    
    private void openOnTheOutside() {
        ...
    }
    private void slide() {
        ...
    }
    
    private enum OpeningMechanism {
        INSIDE,
        OUTSIDE,
        SLIDE
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Some code could be extracted into multiple additional classes. _OpeningMechanism_ could become a rich class. 

Initially just a concept represented only by its state, expanding it can take away some responsibility from the parent class, the _Door._

```java
interface OpeningMechanism {
    void activate(OpeningDirection openingDirection);
}

class TowardsInside implements OpeningMechanism {
    public void activate(OpeningDirection openingDirection) {
        if(openingDirection != OpeningDirection.INSIDE) {            
            throw new BrokenDoorException("Damn!! You strong.");
        }
        openOnTheInside();
    }    
    private void openOnTheInside() {
        ...
    }
}
class TowardsOutside implements OpeningMechanism {
    ...
}
class Sliding implements OpeningMechanism {
    ...
}

class Door {
    private final OpeningMechanism openingMechanism;    
    public Door(OpeningMechanism openingMechanism) {
        this.openingMechanism = openingMechanism;
    }
    
    public void open(OpeningDirection openingDirection) {
        openingMechanism.activate(openingDirection);
    }
```

### When to use composition?

Once the implementation of a class \(e.g. the _Door\)_ becomes to big and the cohesion of it starts to drop, consider extracting big parts of   it into another class. Consider giving, to a set of properties and methods \(that are cohesive in their functionality\), their own class and "marking" them as an abstraction on its own. Consider composition.

#### What about inheritance?

Inheritance could be used in the current examples because the only **feature** that the abstraction that we were building for the concept of a door was to **"open"**. The only state was _openingMechanism_ and the only public method, _.open\(...\)_, was using that. _Maximum cohesion_  could be achieved with that, because the samples are small.

### Multiples features can break inheritance

It is nice to have classes like _NormalDoor_ and _SlidingDoor,_ that incorporate the different versions of _OpeningMechanism_ into them, but what about when we need a _LockingMechanism_ \(with values like _MetalKey_, _Card_, _Biometrics_\) as another feature for that _Door._ Then we would have classes like:

* _MetalKeyNormalDoor_ 
* _MetalKeySlidingDoor_
* _CardNormalDoor_ 
* _CardSlidingDoor_
* _BiometricsNormalDoor_ 
* _BiometricsSlidingDoor_

Hierarchy \(of classes\) cannot support this kind of diversity, not without extra effort \(avoidable effort\)

{% hint style="info" %}
Inheritance is nice, but favor composition.
{% endhint %}

### Bonus question

What example from section _"The core"_ promotes composition?

